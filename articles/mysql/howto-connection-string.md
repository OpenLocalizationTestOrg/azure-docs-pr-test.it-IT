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
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Database tooconnect applicazioni tooAzure per MySQL
Questo documento sono elencati i tipi di stringa di connessione hello supportati dal Database di Azure per MySQL, insieme a esempi e modelli. Nella stringa di connessione potrebbero essere presenti parametri diversi e impostazioni diverse.

- certificato di hello tooobtain, vedere [come tooconfigure SSL](./howto-configure-ssl.md).
- {your_host} = <servername>.mysql.database.azure.com
- {your_user}@{servername} = formato userID per l'autenticazione in modo corretto.  Utilizzo di appena hello userID genererà toofail autenticazione hello.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

In questo esempio, è il nome di server hello `myserver4demo`, nome del database è `wpdb`, nome utente è `WPAdmin`, e la password è `mypassword!2`. Quindi, deve essere la stringa di connessione hello:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Ottenere informazioni dettagliate sulla stringa di connessione hello da hello portale di Azure
In hello [portale di Azure](https://portal.azure.com), recarsi tooyour Database di Azure per il server MySQL e quindi fare clic su **le stringhe di connessione** tooget la stringa di elenco per l'istanza: ![riquadro stringhe di connessione hello in hello Portale di Azure](./media/howto-connection-strings/connection-strings-on-portal.png)

la stringa Hello fornisce informazioni dettagliate, ad esempio driver di hello, server e altri parametri di connessione di database. Modificare questi esempi con i propri parametri, ad esempio nome del database, password e così via. È quindi possibile utilizzare server toohello tooconnect stringa dal codice e applicazioni.

## <a name="next-steps"></a>Passaggi successivi
- Per altre informazioni sulle raccolte di connessioni, vedere [Concepts - Connection libraries](./concepts-connection-libraries.md) (Concetti: raccolte di connessioni).
