---
title: aaaMigrate proprio database di MySQL mediante dump e il ripristino nel Database di Azure per MySQL | Documenti Microsoft
description: In questo articolo vengono illustrati due tooback modi comuni backup e ripristino di database nel Database di Azure per MySQL, utilizzando strumenti quali PHPMyAdmin mysqldump e MySQL Workbench.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: d05d483ff53483df8e005eae2d9a4f8190e8f663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-tooazure-database-for-mysql-using-dump-and-restore"></a>Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL
In questo articolo vengono illustrati due tooback modi comuni backup e ripristino di database nel Database di Azure per MySQL
- Dump e il ripristino da hello della riga di comando (tramite mysqldump) 
- Dump e ripristino con PHPMyAdmin 

## <a name="before-you-begin"></a>Prima di iniziare
toostep tramite questa procedura-tooguide, è necessario toohave:
- [Creare un database di Azure per il server MySQL - portale di Azure](quickstart-create-mysql-server-database-using-azure-portal.md)
- Avere installato su un computer l'utilità della riga di comando [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html).
- MySQL Workbench [MySQL Workbench scaricare](https://dev.mysql.com/downloads/workbench/), Toad, Navicat o altri toodo strumento MySQL di terze parti dump e il ripristino di comandi.

## <a name="use-common-tools"></a>Usare strumenti comuni
Utilizzare i comuni strumenti e utilità, ad esempio tooremotely Workbench di MySQL, mysqldump, Toad o Navicat connettersi e ripristinare i dati nel Database di Azure per MySQL. Utilizzare tali strumenti nel computer client con un toohello tooconnect di connessione internet del Database di Azure per MySQL. Usare una connessione SSL crittografata per le procedure di sicurezza consigliate. Vedere anche [Configure SSL connectivity in Azure Database for MySQL](concepts-ssl-connection-security.md) (Configurare la connettività SSL nel database di Azure per MySQL). Percorso del cloud speciali tooany toomove hello dump file non è necessario durante la migrazione di Database tooAzure per MySQL. 

## <a name="common-uses-for-dump-and-restore"></a>Usi comuni per il dump e ripristino
È possibile utilizzare l'utilità di MySQL come mysqldump e mysqlpump toodump e caricare i database in un MySQL Database di Azure in diversi scenari comuni. In altri scenari, è possibile utilizzare hello [importare ed esportare](concepts-migrate-import-export.md) approccio invece.

- Usa database esegue il dump quando si esegue la migrazione di database intero hello. Questa indicazione può contenere durante lo spostamento di una grande quantità di dati di MySQL o quando si desidera toominimize interruzione del servizio per le applicazioni o siti live. 
-  Assicurarsi che tutte le tabelle nel database di hello usano il motore di archiviazione InnoDB hello durante il caricamento di dati nel Database di Azure per MySQL. Il database di Azure per MySQL supporta solo il motore di archiviazione InnoDB e pertanto non sono supportati motori di archiviazione alternativi. Se le tabelle sono configurate con altri motori di archiviazione, è necessario convertirli in formato di motore hello InnoDB prima della migrazione tooAzure Database per MySQL.
   Ad esempio, se si dispone di WordPress WebApp utilizzando tabelle MyISAM hello, convertire innanzitutto tali tabelle eseguendo la migrazione in formato InnoDB prima del ripristino di Database tooAzure per MySQL. Clausola hello utilizzare `ENGINE=InnoDB` tooset hello motore utilizzato quando si crea una nuova tabella, quindi trasferire i dati di hello in tabella compatibile di hello prima del ripristino hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```
- problemi di qualsiasi compatibilità tooavoid, assicurarsi di hello stessa versione di MySQL è utilizzato nei sistemi di origine e destinazione hello durante il dump di database. Ad esempio, se il server MySQL esistente è versione 5.7, quindi è necessario eseguire la migrazione tooAzure Database MySQL configurato toorun versione 5.7. Hello `mysql_upgrade` comando non funziona in un Database di Azure per il server MySQL e non è supportato. Se è necessario tooupgrade tra le versioni di MySQL, prima di eseguire il dump o esportare il database di una versione inferiore in una versione successiva di MySQL nel proprio ambiente. Eseguire quindi `mysql_upgrade` prima di tentare la migrazione in un database di Azure per MySQL.

## <a name="performance-considerations"></a>Considerazioni sulle prestazioni
toooptimize prestazioni, prendere nota di queste considerazioni durante il dump di database di grandi dimensioni:
-   Hello utilizzare `exclude-triggers` opzione mysqldump durante il dump di database. Escludere i trigger dai comandi dump file tooavoid hello trigger di attivazione durante il ripristino dei dati hello. 
-   Evitare di hello `single-transaction` opzione mysqldump durante il dump di database di dimensioni molto grandi. Dump molte tabelle all'interno di una singola transazione causa di spazio di archiviazione e toobe risorse di memoria utilizzate durante il ripristino e può causare ritardi nelle prestazioni o limitazioni delle risorse.
-   Utilizzare gli inserimenti di multivalore durante il caricamento con un sovraccarico di esecuzione istruzione toominimize SQL durante il dump di database. Quando si usano i file dump generati dall'utilità mysqldump, gli inserimenti multivalore sono abilitati per impostazione predefinita. 
-  Hello utilizzare `order-by-primary` opzione mysqldump durante il dump di database, in modo che i dati di hello viene inserito nello script nell'ordine delle chiavi primarie.
-   Hello utilizzare `disable-keys` opzione mysqldump durante il dump dei dati, vincoli di chiave esterna toodisable prima di caricamento. La disabilitazione dei controlli della chiave esterna offre miglioramenti delle prestazioni. Abilitare i vincoli hello e verificare dati hello dopo hello carico tooensure integrità referenziale.
-   Usare le tabelle partizionate quando appropriato.
-   Caricare i dati in parallelo. Evitare una quantità eccessiva parallelismo causare toohit un limite di risorse e monitorare le risorse utilizzando hello metriche disponibili nel portale di Azure hello. 
-   Hello utilizzare `defer-table-indexes` opzione mysqlpump durante il dump di database, in modo che la creazione dell'indice venga eseguita dopo il caricamento di dati di tabelle.

## <a name="create-a-backup-file-from-hello-command-line-using-mysqldump"></a>Creare un file di backup da hello della riga di comando utilizzando mysqldump
tooback di un database MySQL esistente nel server locale hello o in una macchina virtuale, eseguire hello comando seguente: 
```bash
$ mysqldump --opt -u [uname] -p[pass] [dbname] > [backupfile.sql]
```

Hello parametri tooprovide sono:
- [uname] Username del database 
- [passaggio] hello password per il database (nota non è disponibile spazio tra -p e la password di hello) 
- nome hello [dbname] del database 
- nome del file hello [backupfile.sql] per il backup del database 
- [-opt] hello mysqldump opzione 

Ad esempio, tooback backup di un database denominato 'testdb' sul server MySQL con nome utente hello "testuser" e non testdb_backup.sql file tooa di password, utilizzare hello comando seguente. Hello comando esegue il backup hello `testdb` database in un file denominato `testdb_backup.sql`, che contiene tutte le istruzioni SQL hello necessari toore-creare database hello. 

```bash
$ mysqldump -u root -p testdb > testdb_backup.sql
```
tooselect tabelle specifiche tooback il database di, i nomi delle tabelle di hello elenco separati da spazi. Ad esempio, tooback solo delle tabelle table1 e table2 da hello 'testdb', seguire questo esempio: 
```bash
$ mysqldump -u root -p testdb table1 table2 > testdb_tables_backup.sql
```

tooback di più di un database in una sola volta, utilizzare hello - opzione di database e i nomi dei database di hello elenco separati da spazi. 
```bash
$ mysqldump -u root -p --databases testdb1 testdb3 testdb5 > testdb135_backup.sql 
```
tooback backup di tutti i database di hello in server hello in una sola volta, è consigliabile utilizzare hello - opzione di tutti i database.
```
$ mysqldump -u root -p --all-databases > alldb_backup.sql 
```

## <a name="create-a-database-on-hello-target-azure-database-for-mysql-server"></a>Creare un database nel Database di Azure di destinazione hello per il server MySQL
Creare un database vuoto nel Database di Azure di destinazione hello per MySQL server in cui i dati di hello toomigrate. Utilizzare uno strumento come database di hello toocreate Workbench di MySQL, Toad o Navicat. database Hello può avere hello stesso nome come database hello dati indipendenti hello il dump o è possibile creare un database con un nome diverso.

tooget connessa, trovare le informazioni di connessione di hello nella pagina proprietà hello nel Database di Azure per MySQL.
![Trovare le informazioni di connessione hello in hello portale di Azure](./media/concepts-migrate-dump-restore/1_server-properties-name-login.png)

Aggiungere informazioni di connessione hello nel Workbench di MySQL.
![Stringa di connessione MySQL Workbench](./media/concepts-migrate-dump-restore/2_setup-new-connection.png)


## <a name="restore-your-mysql-database-using-command-line-or-mysql-workbench"></a>Ripristinare il database MySQL mediante una riga di comando o MySQL Workbench
Dopo aver creato il database di destinazione hello, è possibile utilizzare il comando di mysql hello o MySQL Workbench toorestore hello dati hello specifico appena creata del database dal file di dump hello.
```bash
mysql -h [hostname] -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]
```
In questo esempio, ripristinare i dati di hello in hello appena creato database sul Database di Azure di destinazione hello per il server MySQL.
```bash
$ mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p testdb < testdb_backup.sql
```

## <a name="export-using-phpmyadmin"></a>Esportazione mediante PHPMyAdmin
tooexport, è possibile utilizzare phpMyAdmin strumento comune hello, che potrebbe già installato localmente nell'ambiente in uso. tooexport database MySQL tramite PHPMyAdmin:
- Aprire phpMyAdmin.
- Selezionare il database. Fare clic su nome del database nell'elenco a sinistra di hello hello hello. 
- Fare clic su hello **esportare** collegamento. Una nuova pagina viene visualizzato il dump hello tooview del database.
- Nell'area di esportazione hello, fare clic su hello **Seleziona tutto** collegare toochoose hello tabelle nel database. 
- Nell'area di opzioni SQL hello, fare clic su opzioni appropriate hello. 
- Fare clic su hello **salvare come file** opzione compressione corrispondente hello opzione e quindi fare clic su hello **passare** pulsante. Richiesta si toosave hello file in locale verrà visualizzata una finestra di dialogo.

## <a name="import-using-phpmyadmin"></a>Importazione mediante PHPMyAdmin
Importare il database è tooexporting simile. Hello le seguenti operazioni:
- Aprire phpMyAdmin. 
- Nella pagina di installazione phpMyAdmin hello, fare clic su **Aggiungi** tooadd del Database di Azure per il server MySQL. Fornire i dettagli della connessione hello e informazioni di accesso.
- Creare un database denominato in modo appropriato e selezionarlo in a sinistra della schermata di hello hello. toorewrite hello database esistente, fare clic sul nome di database hello, selezionare tutte le caselle di controllo hello accanto a nomi di tabella hello e selezionare **Drop** toodelete hello tabelle esistenti. 
- Fare clic su hello **SQL** collegamento tooshow hello la pagina in cui è possibile digitare nei comandi SQL o caricare il file SQL. 
- Hello utilizzare **Sfoglia** file di database hello toofind pulsante. 
- Fare clic su hello **passare** pulsante backup hello tooexport, eseguire i comandi SQL hello e ricreare il database.

## <a name="next-steps"></a>Passaggi successivi
[La connessione applicazioni tooAzure Database MySQL](./howto-connection-string.md)
