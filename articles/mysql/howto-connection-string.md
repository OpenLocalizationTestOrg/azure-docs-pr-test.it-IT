---
title: aaaConnect applicazioni tooAzure Database per MySQL | Documenti Microsoft
description: Questo documento vengono elencate le stringhe di connessione hello attualmente supportato per le applicazioni tooconnect con Database di Azure per MySQL, incluso ADO.NET (c#), JDBC, Node.js, ODBC, PHP, Python e Ruby.
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="afe34-103">Database tooconnect applicazioni tooAzure per MySQL</span><span class="sxs-lookup"><span data-stu-id="afe34-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="afe34-104">Questo documento sono elencati i tipi di stringa di connessione hello supportati dal Database di Azure per MySQL, insieme a esempi e modelli.</span><span class="sxs-lookup"><span data-stu-id="afe34-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="afe34-105">Nella stringa di connessione potrebbero essere presenti parametri diversi e impostazioni diverse.</span><span class="sxs-lookup"><span data-stu-id="afe34-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="afe34-106">certificato di hello tooobtain, vedere [come tooconfigure SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="afe34-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="afe34-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="afe34-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="afe34-108">{your_user}@{servername} = formato userID per l'autenticazione in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="afe34-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="afe34-109">Utilizzo di appena hello userID genererà toofail autenticazione hello.</span><span class="sxs-lookup"><span data-stu-id="afe34-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="afe34-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="afe34-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="afe34-111">In questo esempio, è il nome di server hello `myserver4demo`, nome del database è `wpdb`, nome utente è `WPAdmin`, e la password è `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="afe34-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="afe34-112">Quindi, deve essere la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="afe34-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="afe34-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="afe34-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="afe34-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="afe34-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="afe34-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="afe34-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="afe34-116">PHP</span><span class="sxs-lookup"><span data-stu-id="afe34-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="afe34-117">Python</span><span class="sxs-lookup"><span data-stu-id="afe34-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="afe34-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="afe34-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="afe34-119">Ottenere informazioni dettagliate sulla stringa di connessione hello da hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="afe34-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="afe34-120">In hello [portale di Azure](https://portal.azure.com), recarsi tooyour Database di Azure per il server MySQL e quindi fare clic su **le stringhe di connessione** tooget la stringa di elenco per l'istanza: ![riquadro stringhe di connessione hello in hello Portale di Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="afe34-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="afe34-121">la stringa Hello fornisce informazioni dettagliate, ad esempio driver di hello, server e altri parametri di connessione di database.</span><span class="sxs-lookup"><span data-stu-id="afe34-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="afe34-122">Modificare questi esempi con i propri parametri, ad esempio nome del database, password e così via.</span><span class="sxs-lookup"><span data-stu-id="afe34-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="afe34-123">È quindi possibile utilizzare server toohello tooconnect stringa dal codice e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="afe34-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afe34-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afe34-124">Next steps</span></span>
- <span data-ttu-id="afe34-125">Per altre informazioni sulle raccolte di connessioni, vedere [Concepts - Connection libraries](./concepts-connection-libraries.md) (Concetti: raccolte di connessioni).</span><span class="sxs-lookup"><span data-stu-id="afe34-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
