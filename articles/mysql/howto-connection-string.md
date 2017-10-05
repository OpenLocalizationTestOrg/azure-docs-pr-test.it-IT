---
title: Connettere le applicazioni a Database di Azure per MySQL | Microsoft Docs
description: Questo documento elenca le stringhe di connessione attualmente supportate per consentire alle applicazioni di connettersi a Database di Azure per MySQL, tra cui ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python e Ruby.
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="87a64-103">Come connettere le applicazioni a Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="87a64-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="87a64-104">Questo documento elenca i tipi di stringa di connessione supportati da Database di Azure per MySQL, oltre a modelli ed esempi.</span><span class="sxs-lookup"><span data-stu-id="87a64-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="87a64-105">Nella stringa di connessione potrebbero essere presenti parametri diversi e impostazioni diverse.</span><span class="sxs-lookup"><span data-stu-id="87a64-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="87a64-106">Per ottenere il certificato, vedere [Come configurare SSL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="87a64-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="87a64-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="87a64-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="87a64-108">{your_user}@{servername} = formato userID per l'autenticazione in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="87a64-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="87a64-109">Se si usa solo userID, l'autenticazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="87a64-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="87a64-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="87a64-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="87a64-111">In questo esempio il nome del server è `myserver4demo`, il nome del database è `wpdb`, il nome utente è `WPAdmin` e la password è `mypassword!2`.</span><span class="sxs-lookup"><span data-stu-id="87a64-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="87a64-112">La stringa di connessione sarà quindi:</span><span class="sxs-lookup"><span data-stu-id="87a64-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="87a64-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="87a64-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="87a64-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="87a64-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="87a64-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="87a64-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="87a64-116">PHP</span><span class="sxs-lookup"><span data-stu-id="87a64-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="87a64-117">Python</span><span class="sxs-lookup"><span data-stu-id="87a64-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="87a64-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="87a64-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="87a64-119">Ottenere i dettagli della stringa di connessione dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="87a64-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="87a64-120">Nel [portale di Azure](https://portal.azure.com) andare al database di Azure per il server MySQL e quindi fare clic su **Stringhe di connessione** per ottenere l'elenco di stringhe per l'istanza: ![il riquadro Stringhe di connessione nel portale di Azure](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="87a64-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="87a64-121">La stringa include informazioni dettagliate quali il driver, il server e altri parametri di connessione al database.</span><span class="sxs-lookup"><span data-stu-id="87a64-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="87a64-122">Modificare questi esempi con i propri parametri, ad esempio nome del database, password e così via.</span><span class="sxs-lookup"><span data-stu-id="87a64-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="87a64-123">È quindi possibile usare questa stringa per la connessione al server dal codice e dalle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="87a64-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87a64-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87a64-124">Next steps</span></span>
- <span data-ttu-id="87a64-125">Per altre informazioni sulle raccolte di connessioni, vedere [Concepts - Connection libraries](./concepts-connection-libraries.md) (Concetti: raccolte di connessioni).</span><span class="sxs-lookup"><span data-stu-id="87a64-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
