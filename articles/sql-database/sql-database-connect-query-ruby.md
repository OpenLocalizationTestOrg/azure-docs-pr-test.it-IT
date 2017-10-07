---
title: aaaUse tooquery Ruby Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse toocreate Ruby un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 94fec528-58ba-4352-ba0d-25ae4b273e90
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: carlrab
ms.openlocfilehash: 0d4b16b8aacb5e376ab80cbe37569130f2fd52b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ruby-tooquery-an-azure-sql-database"></a>Utilizzare tooquery Ruby un database SQL di Azure

Questa esercitazione introduttiva illustra come toouse [Ruby](https://www.ruby-lang.org) toocreate un tooan tooconnect programma Azure SQL database e utilizzare dati tooquery di istruzioni Transact-SQL.

## <a name="prerequisites"></a>Prerequisiti

Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere hello seguenti prerequisiti:

- un database SQL di Azure. Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive: 

   - [Creare un database: portale](sql-database-get-started-portal.md)
   - [Creare un database: interfaccia della riga di comando](sql-database-get-started-cli.md)
   - [Creare un database: PowerShell](sql-database-get-started-powershell.md)

- Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.
- Avere installato Ruby e il software correlato per il sistema operativo.
    - **MacOS**: installare Homebrew, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS. Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/).
    - **Ubuntu**: installare i prerequisiti per Ruby, installare rbenv e ruby-build, installare Ruby e quindi installare FreeTDS. Vedere i [passaggi 1.2, 1.3, 1.4 e 1.5](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu/).

## <a name="sql-server-connection-information"></a>Informazioni di connessione SQL Server

Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect. Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina. 
3. In hello **Panoramica** pagina per il database, esaminare hello nome completo del server. È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione, come illustrato nella seguente immagine hello:

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Se si hanno dimenticato di informazioni di accesso hello del server di Database SQL di Azure, passare toohello Database di SQL server pagina tooview hello admin nome del server e, se necessario, reimpostare la password di hello.

> [!IMPORTANT]
> Sul posto per l'indirizzo IP pubblico hello del computer hello in cui si esegue questa esercitazione, è necessario disporre una regola del firewall. Se in un computer diverso o di un diverso indirizzo IP pubblico, creare un [regola firewall di livello server utilizzando il portale di Azure di hello](sql-database-get-started-portal.md#create-a-server-level-firewall-rule). 

## <a name="insert-code-tooquery-sql-database"></a>Inserire codice tooquery SQL database

1. Nell'editor di testo preferito creare un nuovo file, **sqltest.rb**.

2. Sostituire il contenuto di hello con hello seguente di codice e aggiungere hello valori appropriati per il server, database, l'utente e password.

```ruby
require 'tiny_tds'
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
client = TinyTds::Client.new username: username, password: password, 
    host: server, port: 1433, database: database, azure: true

puts "Reading data from table"
tsql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
        FROM [SalesLT].[ProductCategory] pc
        JOIN [SalesLT].[Product] p
        ON pc.productcategoryid = p.productcategoryid"
result = client.execute(tsql)
result.each do |row|
    puts row
end
```

## <a name="run-hello-code"></a>Eseguire il codice hello

1. Al prompt dei comandi di hello, eseguire hello seguenti comandi:

   ```bash
   ruby sqltest.rb
   ```

2. Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.


## <a name="next-steps"></a>Passaggi successivi
- [Progettare il primo database SQL di Azure](sql-database-design-first-database.md)
- [Repository GitHub per TinyTDS](https://github.com/rails-sqlserver/tiny_tds)
- [Segnalare problemi o porre domande su TinyTDS](https://github.com/rails-sqlserver/tiny_tds/issues)
- [Driver Ruby per SQL Server](https://docs.microsoft.com/sql/connect/ruby/ruby-driver-for-sql-server/)
