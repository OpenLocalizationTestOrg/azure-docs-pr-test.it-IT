---
title: La connessione tooAzure Database MySQL da c# | Documenti Microsoft
description: "Questa Guida rapida viene fornito un esempio codice c# (.NET) è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati tooconnect e query di utilizzo di .NET (c#)
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di un'applicazione c# di MySQL. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. Hello passaggi in questo articolo si presuppone che si abbia familiarità con lo sviluppo in c#, e che siano tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

È anche necessario:
- Installare [.NET](https://www.microsoft.com/net/download). Seguire passaggi hello hello collegato articolo tooinstall .NET in modo specifico per la piattaforma (Windows, Ubuntu Linux o Mac OS). 
- [Installare Visual Studio](https://www.visualstudio.com/downloads/).
- Installare il [driver ODBC per MySQL](https://dev.mysql.com/downloads/connector/odbc/).

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.
3. Fare clic su nome hello del server.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Nome del server del database di Azure per MySQL](./media/connect-csharp/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL. codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione. Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello. 

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a>Leggere i dati

Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione. Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) e metodo [ExecuteReader](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun i comandi di database hello. Successivamente hello viene utilizzato codice [Read](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello record nei risultati di hello. Codice hello Usa quindi i valori hello tooparse GetInt32 e GetString nel record di hello.

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL. codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione. Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello.

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect ed eliminare hello dati utilizzando un **eliminare** istruzione SQL. 

codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione. Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello.

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL](concepts-migrate-dump-restore.md)
