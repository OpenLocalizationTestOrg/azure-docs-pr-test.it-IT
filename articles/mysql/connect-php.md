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
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="4e26d-103">Il Database di Azure per MySQL: dati di utilizzo PHP tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="4e26d-103">Azure Database for MySQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="4e26d-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL un [PHP](http://php.net/manual/intro-whatis.php) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4e26d-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="4e26d-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="4e26d-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="4e26d-106">In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite PHP, ma che sono tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e26d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e26d-107">Prerequisites</span></span>
<span data-ttu-id="4e26d-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="4e26d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="4e26d-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="4e26d-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="4e26d-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4e26d-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="4e26d-111">Installare PHP</span><span class="sxs-lookup"><span data-stu-id="4e26d-111">Install PHP</span></span>
<span data-ttu-id="4e26d-112">Installare PHP nel server o creare un'[app Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) di Azure che includa PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="macos"></a><span data-ttu-id="4e26d-113">MacOS</span><span class="sxs-lookup"><span data-stu-id="4e26d-113">MacOS</span></span>
- <span data-ttu-id="4e26d-114">Scaricare [PHP versione 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="4e26d-114">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="4e26d-115">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.macosx.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="4e26d-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="4e26d-116">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="4e26d-116">Linux (Ubuntu)</span></span>
- <span data-ttu-id="4e26d-117">Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="4e26d-117">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="4e26d-118">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.unix.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="4e26d-118">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>

### <a name="windows"></a><span data-ttu-id="4e26d-119">Windows</span><span class="sxs-lookup"><span data-stu-id="4e26d-119">Windows</span></span>
- <span data-ttu-id="4e26d-120">Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="4e26d-120">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="4e26d-121">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.windows.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="4e26d-121">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="4e26d-122">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="4e26d-122">Get connection information</span></span>
<span data-ttu-id="4e26d-123">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-123">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="4e26d-124">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="4e26d-124">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="4e26d-125">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4e26d-125">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4e26d-126">Nel riquadro di sinistra hello, fare clic su **tutte le risorse**e quindi cercare server hello sia stato creato (ad esempio, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="4e26d-126">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="4e26d-127">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="4e26d-127">Click hello server name.</span></span>
4. <span data-ttu-id="4e26d-128">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="4e26d-128">Select hello server's **Properties** page.</span></span> <span data-ttu-id="4e26d-129">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="4e26d-129">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="4e26d-130">![Nome del server del database di Azure per MySQL](./media/connect-php/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="4e26d-130">![Azure Database for MySQL server name](./media/connect-php/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="4e26d-131">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="4e26d-131">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="4e26d-132">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="4e26d-132">Connect and create a table</span></span>
<span data-ttu-id="4e26d-133">Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-133">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement.</span></span> 

<span data-ttu-id="4e26d-134">codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-134">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4e26d-135">metodi di chiamata di codice Hello [mysqli_init](http://php.net/manual/mysqli.init.php) e [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-135">hello code call methods [mysqli_init](http://php.net/manual/mysqli.init.php) and [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL.</span></span> <span data-ttu-id="4e26d-136">Viene quindi chiamato metodo [mysqli_query](http://php.net/manual/mysqli.query.php) query hello toorun.</span><span class="sxs-lookup"><span data-stu-id="4e26d-136">Then it calls method [mysqli_query](http://php.net/manual/mysqli.query.php) toorun hello query.</span></span> <span data-ttu-id="4e26d-137">Viene quindi chiamato metodo [mysqli_close](http://php.net/manual/mysqli.close.php) connessione hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="4e26d-137">Then it calls method [mysqli_close](http://php.net/manual/mysqli.close.php) tooclose hello connection.</span></span>

<span data-ttu-id="4e26d-138">Sostituire i parametri di host, username, password e db_name hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4e26d-138">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="insert-data"></a><span data-ttu-id="4e26d-139">Inserire dati</span><span class="sxs-lookup"><span data-stu-id="4e26d-139">Insert data</span></span>
<span data-ttu-id="4e26d-140">Seguente hello utilizzare codice tooconnect e inserire dati utilizzando un **inserire** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-140">Use hello following code tooconnect and insert data using an **INSERT** SQL statement.</span></span>

<span data-ttu-id="4e26d-141">codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-141">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4e26d-142">codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una istruzione insert, quindi associa hello parametri per ogni valore della colonna inserita con metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-142">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared insert statement, then binds hello parameters for each inserted column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4e26d-143">codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-143">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4e26d-144">Sostituire i parametri di host, username, password e db_name hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4e26d-144">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="4e26d-145">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="4e26d-145">Read data</span></span>
<span data-ttu-id="4e26d-146">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-146">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span>  <span data-ttu-id="4e26d-147">codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-147">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4e26d-148">codice Hello Usa metodo [mysqli_query](http://php.net/manual/mysqli.query.php) eseguire query sql hello e utilizza [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch metodo hello righe risultanti.</span><span class="sxs-lookup"><span data-stu-id="4e26d-148">hello code uses method [mysqli_query](http://php.net/manual/mysqli.query.php) perform hello sql query, and uses [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) method toofetch hello resulting rows.</span></span>

<span data-ttu-id="4e26d-149">Sostituire i parametri di host, username, password e db_name hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4e26d-149">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="4e26d-150">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="4e26d-150">Update data</span></span>
<span data-ttu-id="4e26d-151">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-151">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="4e26d-152">codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-152">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4e26d-153">codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate un'istruzione update preparata, quindi associa parametri hello per il valore di ogni colonna aggiornata con metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-153">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared update statement, then binds hello parameters for each updated column value using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4e26d-154">codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-154">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4e26d-155">Sostituire i parametri di host, username, password e db_name hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4e26d-155">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="4e26d-156">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="4e26d-156">Delete data</span></span>
<span data-ttu-id="4e26d-157">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="4e26d-157">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="4e26d-158">codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP.</span><span class="sxs-lookup"><span data-stu-id="4e26d-158">hello code uses hello **MySQL Improved extension** (mysqli) class included in PHP.</span></span> <span data-ttu-id="4e26d-159">codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una istruzione delete, quindi associa hello parametri per hello dove clausola nell'istruzione hello metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-159">hello code uses method [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate a prepared delete statement, then binds hello parameters for hello where clause in hello statement using method [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php).</span></span> <span data-ttu-id="4e26d-160">codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span><span class="sxs-lookup"><span data-stu-id="4e26d-160">hello code runs hello statement using method [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) and afterwards closes hello statement using method [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).</span></span>

<span data-ttu-id="4e26d-161">Sostituire i parametri di host, username, password e db_name hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4e26d-161">Replace hello host, username, password, and db_name parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="4e26d-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e26d-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4e26d-163">Creare un'app Web PHP e MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="4e26d-163">Build a PHP and MySQL web app in Azure</span></span>](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
