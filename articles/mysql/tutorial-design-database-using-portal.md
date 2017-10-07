---
title: aaaDesign di Azure prima di Database per database MySQL - portale di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato come toocreate e gestire i Database di Azure per il server MySQL e di database tramite il portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a>Progettare il primo database di Azure per il database MySQL
Il Database di Azure per MySQL è un servizio gestito che consente di toorun, gestire e scalare il database MySQL a disponibilità elevata nel cloud hello. Utilizza hello portale di Azure, è possibile facilmente gestire il server e progettare un database.

In questa esercitazione, utilizzare la modalità hello toolearn portale Azure per:

> [!div class="checklist"]
> * Creare un database di Azure per MySQL
> * Configurare firewall hello del server
> * Utilizzare lo strumento da riga di comando di mysql toocreate un database
> * Caricare dati di esempio
> * Eseguire query sui dati
> * Aggiornare i dati
> * Ripristinare i dati

## <a name="sign-in-toohello-azure-portal"></a>Accedi toohello portale di Azure
Aprire il browser web preferite e visitare hello [portale Microsoft Azure](https://portal.azure.com/). Immettere le credenziali toosign nel portale toohello. visualizzazione predefinita Hello è il dashboard del servizio.

## <a name="create-an-azure-database-for-mysql-server"></a>Creare un database di Azure per il server MySQL
Verrà creato un database di Azure per MySQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md). Hello server viene creato all'interno di un [gruppo di risorse](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

1. Passare troppo**database** > **Database di Azure per MySQL**. Se non si trova il MySQL Server con **database** categoria, fare clic su **tutti** tooshow tutti disponibili servizi di database. È anche possibile digitare **Database di Azure per MySQL** nel tooquickly casella di ricerca hello individuare hello servizio.
![2-1 Naviga tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)

2. Fare clic sul riquadro **Database di Azure per MySQL** e quindi fare clic su **Crea**.

In questo esempio, compilare hello Azure Database MySQL form con hello le seguenti informazioni:

| **Impostazione** | **Valore consigliato** | **Descrizione campo** |
|---|---|---|
| *Server name* (Nome server) | myserver4demo  | Nome del server ha toobe univoco globale. |
| *Sottoscrizione* | mysubscription | Selezionare la sottoscrizione dall'elenco a discesa hello. |
| *Gruppo di risorse* | myresourcegroup | Creare un gruppo di risorse o usarne uno esistente. |
| *Nome di accesso amministratore server* | myadmin | Configurare il nome dell'account amministratore. |
| *Password* |  | Impostare una password complessa per l'account amministratore. |
| *Conferma password* |  | Conferma password dell'account admin hello. |
| *Posizione* |  | Selezionare un'area disponibile. |
| *Versione* | 5.7 | Scegliere la versione più recente di hello. |
| *Configura prestazioni* | Base con 50 unità di calcolo, 50 GB  | Scegliere **Piano tariffario**, **Unità di calcolo**, **Archiviazione (GB)** e quindi fare clic su **OK**. |
| *PIN tooDashboard* | Controllo | Consigliato toocheck questa casella, pertanto è possibile che il server di hello facilmente in un secondo momento |
Fare quindi clic su **Crea**. In uno o due minuti, un nuovo Database di Azure per il server MySQL è in esecuzione nel cloud hello. È possibile fare clic su **notifiche** pulsante nel processo di distribuzione hello toomonitor hello barra degli strumenti.

## <a name="configure-firewall"></a>Configurare il firewall
I database di Azure per MySQL sono protetti da un firewall. Per impostazione predefinita, tutte le connessioni toohello database e server hello all'interno di server hello vengono rifiutati. Prima connessione tooAzure Database MySQL per hello prima volta, configurare l'indirizzo IP di rete pubblica hello firewall tooadd hello del computer client (o intervallo di indirizzi IP).

1. Fare clic sul server appena creato e quindi fare clic su **Sicurezza connessione**.
   ![3-1 Sicurezza della connessione](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)
2. È possibile scegliere **Aggiungi indirizzo IP corrente** o configurare le regole del firewall qui. Ricordare tooclick **salvare** dopo aver creato le regole di hello.
È ora possibile connettersi a server toohello strumento della riga di comando di mysql o MySQL Workbench GUI.

> [!TIP]
> Il Database di Azure per il server MySQL comunica sulla porta 3306. Se si sta tentando di tooconnect da una rete aziendale, il traffico in uscita sulla porta 3306 può non essere consentito dal firewall della rete. In questo caso, è possibile connettersi tooAzure MySQL server, a meno che il reparto IT apre la porta 3306.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Get hello completo **nome Server** e **nome account di accesso di amministratore Server** per il Database di Azure per il server MySQL da hello portale di Azure. Utilizzare hello server completo tooconnect tooyour server dei nomi utilizzando lo strumento da riga di comando di mysql. 

1. In [portale di Azure](https://portal.azure.com/), fare clic su **tutte le risorse** dal menu a sinistra di hello, nome del tipo hello e ricerca per il Database di Azure per il server MySQL. Selezionare i dettagli di hello tooview nome server hello.

2. In impostazioni hello fare clic su **proprietà**. Prendere nota del **NOME SERVER** e del **NOME DI ACCESSO DELL'AMMINISTRATORE SERVER**. È possibile fare clic su hello copia pulsante Avanti tooeach campo toocopy toohello negli Appunti.
   ![4-2 Proprietà del server](./media/tutorial-design-database-using-portal/4_2-server-properties.png)

In questo esempio, è il nome di server hello *myserver4demo.mysql.database.azure.com*, e l'account di accesso amministratore server hello è  *myadmin@myserver4demo* .

## <a name="connect-toohello-server-using-mysql"></a>Connessione server toohello con mysql
Utilizzare [lo strumento da riga di comando di mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour una connessione Database di Azure per il server MySQL. È possibile eseguire lo strumento da riga di comando di mysql hello da hello Azure Cloud Shell nel browser hello o dal computer utilizzando gli strumenti di mysql installati localmente. hello toolaunch Shell di Cloud di Azure, fare clic su hello `Try It` pulsante in un blocco di codice in questo articolo, o visitare il portale di Azure hello e fare clic su hello `>_` icona in hello superiore destro della barra degli strumenti. 

Digitare tooconnect comando hello:
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a>Creazione di un database vuoto
Dopo aver connesso toohello server, creare un database vuoto di toowork con.
```sql
CREATE DATABASE mysampledb;
```

Al prompt dei comandi hello, eseguire hello database toothis appena creati connessione tooswitch di comando seguente:
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a>Creare tabelle nel database di hello
Ora che è stato appreso come tooconnect toohello Database di Azure per il database MySQL, possiamo andare come toocomplete alcune attività di base.

In primo luogo, è possibile creare una tabella e caricarla con alcuni dati. Creare una tabella che contenga le informazioni riguardanti l'inventario.
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a>Caricamento dei dati nelle tabelle di hello
Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno. Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati.
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

Ora si dispone di due righe di dati di esempio nella tabella hello creato in precedenza.

## <a name="query-and-update-hello-data-in-hello-tables"></a>Eseguire una query e aggiornare i dati nelle tabelle di hello hello
Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.
```sql
SELECT * FROM inventory;
```

È inoltre possibile aggiornare i dati di hello nelle tabelle di hello.
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a>Ripristinare un punto precedente tooa di database nel tempo
Si supponga di essere eliminato per una tabella di database più importanti e non è possibile ripristinare facilmente i dati di hello. Il Database di Azure per MySQL consente toorestore hello server tooa punto nel tempo, creazione di una copia dei database hello nel nuovo server. È possibile utilizzare questo nuovo toorecover server i dati eliminati. Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.

1. Nel portale di Azure hello, individuare il Database di Azure per MySQL. In hello **Panoramica** pagina, fare clic su **ripristinare** sulla barra degli strumenti hello. verrà visualizzata la pagina ripristino Hello.

   ![10-1 Ripristinare un database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. Compilare hello **ripristinare** form con le informazioni necessarie hello.
   
   ![10-2 Modulo di ripristino](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - **Punto di ripristino**: selezionare un punto-in-time che si desidera toorestore, entro il periodo di hello elencato. Verificare che tooconvert tooUTC il fuso orario locale.
   - **Ripristinare il server toonew**: fornire un nuovo nome del server desiderato toorestore per.
   - **Percorso**: hello area è lo stesso server di origine hello e non può essere modificato.
   - **Livello di prezzo**: hello tariffario è hello equivale hello server di origine e non può essere modificati.
   
3. Fare clic su **OK** toorestore hello server troppo[tooa punto di ripristino temporizzato](./howto-restore-server-portal.md) prima tabella hello è stata eliminata. Ripristino di un server crea una nuova copia del server di hello, a partire da hello punto nel tempo specificato. 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, utilizzare la modalità hello toolearned portale Azure per:

> [!div class="checklist"]
> * Creare un database di Azure per MySQL
> * Configurare firewall hello del server
> * Utilizzare lo strumento da riga di comando di mysql toocreate un database
> * Caricare dati di esempio
> * Eseguire query sui dati
> * Aggiornare i dati
> * Ripristinare i dati

> [!div class="nextstepaction"]
> [Database tooconnect applicazioni tooAzure per MySQL](./howto-connection-string.md)
