---
title: La connessione tooAzure Database MySQL da MySQL Workbench | Documenti Microsoft
description: Questa Guida rapida fornisce hello passaggi toouse MySQL Workbench tooconnect ed eseguire query sui dati dal Database di Azure per MySQL.
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati di utilizzo MySQL Workbench tooconnect e query
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL hello applicazione Workbench di MySQL. 

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-mysql-workbench"></a>Installare MySQL Workbench
Scaricare e installare MySQL Workbench nel computer in uso da [sito Web di MySQL hello](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).

2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.

3. Fare clic su nome hello del server.

4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.

 ![Nome del server del database di Azure per MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Connessione server toohello utilizzando Workbench di MySQL 
utilizzo dello strumento GUI hello Workbench di MySQL server tooconnect tooAzure MySQL:

1.  Avviare hello applicazione Workbench di MySQL nel computer in uso. 

2.  In **il programma di installazione nuova connessione** finestra di dialogo immettere le seguenti informazioni su hello hello **parametri** scheda:

    ![Setup New Connection (Configura nuova connessione)](./media/connect-workbench/2-setup-new-connection.png)

    | **Impostazione** | **Valore consigliato** | **Descrizione campo** |
    |---|---|---|
    |   Connection Name (Nome connessione) | Demo Connection | Specificare un'etichetta per la connessione. |
    | Connection Method (Metodo di connessione) | Standard (TCP/IP) | Standard (TCP/IP) è sufficiente. |
    | Nome host | *nome del server* | Specificare hello server valore del nome è stato utilizzato durante la creazione hello Database di Azure per MySQL in precedenza. Il server di esempio visualizzato è myserver4demo.mysql.database.azure.com. Utilizza il nome di dominio completo hello (\*. mysql.database.azure.com) come illustrato nell'esempio hello. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda il nome del server.  |
    | Porta | 3306 | Utilizzare sempre porta 3306 durante la connessione di Database tooAzure per MySQL. |
    | Username |  *nome di accesso amministratore server* | Digitare nome utente account di accesso amministratore server hello specificato durante la creazione del Database di Azure hello per MySQL in precedenza. Il nome utente dell'esempio è myadmin@myserver4demo. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda hello username. formato hello è  *username@servername* .
    | Password | Immettere la password. | Fare clic su **archivio nell'insieme di credenziali...**  password hello toosave di pulsante. |

3.   Fare clic su **Test connessione** tootest se tutti i parametri siano configurati correttamente. 

4.   Fare clic su **OK** connessione hello toosave. 

5.   Nell'elenco di hello di **connessioni MySQL**, fare clic su server tooyour corrispondente di hello riquadro e attendere hello toobe di connessione stabilita.

6.   Verrà visualizzata una nuova scheda SQL con un editor vuoto in cui è possibile digitare le query.

    > [!NOTE]
    > Per impostazione predefinita, in Database di Azure per il server MySQL è necessaria e viene applicata la sicurezza della connessione SSL. In genere alcuna configurazione aggiuntiva con i certificati SSL non è necessario per tooyour tooconnect del Workbench di MySQL server. Per ulteriori informazioni su SSL, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md).  Se è necessario toodisable SSL, visitare il portale di Azure hello e fare clic su hello connessione sicurezza pagina toodisable hello applicare SSL connessione interruttore.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Creare una tabella e inserire, leggere, aggiornare ed eliminare dati
1. Copiare e incollare hello SQL esempio un vuoto tooillustrate scheda SQL alcuni dati di esempio.

    Il codice crea un database vuoto denominato quickstartdb, quindi crea una tabella di esempio denominata inventory. Consente di inserire alcune righe, quindi legge righe hello. Modifica dati hello con un'istruzione update e letture hello righe nuovamente. Infine viene eliminata una riga e legge le righe di hello nuovamente.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    schermata di Hello illustra un esempio di codice SQL hello nell'output di SQL Workbench e hello dopo che è stato eseguito.
    
    ![Codice SQL di esempio toorun scheda SQL Workbench di MySQL](media/connect-workbench/3-workbench-sql-tab.png)

2. esempio hello toorun codice SQL, fare clic su hello schiarire sull'icona nella barra degli strumenti hello di hello **File SQL** scheda.
3. Si noti hello tre risultati a schede in hello **griglia dei risultati** sezione della pagina hello intermedio hello. 
4. Hello preavviso **Output** elenco hello parte inferiore della pagina hello. viene visualizzato lo stato di Hello di ogni comando. 

A questo punto, si è connessi tooAzure Database per MySQL mediante MySQL Workbench e dati usando il linguaggio SQL hello sono sottoposti a query.

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./concepts-migrate-import-export.md)
