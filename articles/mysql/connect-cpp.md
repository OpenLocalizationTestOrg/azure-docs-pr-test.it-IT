---
title: La connessione tooAzure Database MySQL da C++ | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice C++, è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati tooconnect e query di utilizzare connettore/C++
Questa Guida introduttiva illustra come Database di Azure tooconnect tooan per MySQL mediante un'applicazione C++. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. Hello passaggi in questo articolo si presuppone che si ha familiarità con lo sviluppo usando C++ e che siano tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

È anche necessario:
- Installare [.NET Framework](https://www.microsoft.com/net/download)
- Installare [Visual Studio](https://www.visualstudio.com/downloads/)
- Installare [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) 
- Installare [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>Installare Visual Studio e .NET
passaggi di Hello in questa sezione si presuppongono che si abbia familiarità con lo sviluppo con .NET.

### <a name="windows"></a>**Windows**
1. Installare Visual Studio 2017 Community, che è un IDE gratuito, con funzionalità complete ed estendibile per creare applicazioni moderne per Android, iOS, Windows, oltre ad applicazioni Web e database e servizi cloud. È possibile installare hello completa di .NET Framework o solo a .NET Core. frammenti di codice Hello hello Guida introduttiva di lavoro con uno. Se si dispone già di Visual Studio installati nel computer, ignorare hello due passaggi successivi.
   - Scaricare hello [programma di installazione di Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Eseguire il programma di installazione hello e seguire hello installazione richieste toocomplete hello installazione.

### <a name="configure-visual-studio"></a>**Configurare Visual Studio**
1. Da Visual Studio, proprietà del progetto > proprietà di configurazione > C/C++ > linker > generale > Directory librerie aggiuntive, aggiungere directory lib\opt hello (ad esempio: C:\Program Files (x86) \MySQL\MySQL connettore C++ 1.1.9\lib\opt) di hello c + + connettore.
2. Da Visual Studio, Proprietà progetto > Proprietà di configurazione > C/C++ > Generale > Directory di inclusione aggiuntive
   - Aggiungere la directory include/ del connettore C++ (ad esempio: C:\Programmi (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - Aggiungere la directory radice della libreria Boost (ad esempio: C:\boost_1_64_0\)
3. Da Visual Studio, proprietà del progetto > proprietà di configurazione > C/C++ > linker > Input > dipendenze aggiuntive, aggiungere mysqlcppconn.lib nel campo di testo hello
4. Entrambi mysqlcppconn.dll copia dalla hello c + + connettore cartella libreria nel passaggio 3 toohello stessa directory del file eseguibile dell'applicazione hello o aggiungere la variabile di ambiente toohello poterlo trovare l'applicazione.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.
3. Fare clic su nome hello del server.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Nome del server del database di Azure per MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL. codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione. Codice hello utilizza quindi metodo Execute () e createStatement() toorun hello i comandi di database. 

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a>Leggere i dati

Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione. Quindi codice hello Usa metodo prepareStatement() ed executeQuery() toorun hello selezionare comandi. Codice di hello utilizzerà infine Next tooadvance toohello record nei risultati di hello. Codice hello Usa quindi i valori hello tooparse getInt() e GetString () nel record di hello.

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL. codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione. Codice hello utilizza quindi metodo prepareStatement() ed executeQuery() toorun hello i comandi di aggiornamento. 

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione. Usa metodo prepareStatement() quindi codice hello executeQuery() toorun hello comandi e delete.

Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL](concepts-migrate-dump-restore.md)
