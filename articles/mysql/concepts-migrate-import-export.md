---
title: aaaImport e l'esportazione nel Database di Azure per MySQL | Documenti Microsoft
description: Questo articolo illustra modi tooimport ed esportazione database comuni nel Database di Azure per MySQL, mediante strumenti quali Workbench di MySQL.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: e2c036773d975df2eea2a59d166ea10567218a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-mysql-database-by-using-import-and-export"></a>Migrare il database MySQL mediante l'importazione ed esportazione
Questo articolo illustra due tooimporting approcci comuni e l'esportazione dei dati tooan Database di Azure per il server MySQL con MySQL Workbench. 

## <a name="before-you-begin"></a>Prima di iniziare
toostep tramite questa procedura-tooguide, è necessario:
- Un database di Azure per il server MySQL, seguendo la procedura descritta in [Creare un database di Azure per il server MySQL tramite il portale di Azure](quickstart-create-mysql-server-database-using-azure-portal.md).
- MySQL Workbench [scaricato](https://dev.mysql.com/downloads/workbench/), o un altro tooimport strumento MySQL e l'esportazione.

## <a name="use-common-tools"></a>Usare strumenti comuni
Utilizzare gli strumenti comuni, ad esempio tooremotely Workbench di MySQL, Toad o Navicat connettersi e importare o esportare dati in Database di Azure per MySQL. 

Utilizzare tali strumenti nel computer client con un tooAzure tooconnect di connessione Internet del Database per MySQL. Usare una connessione SSL crittografata per le procedure di sicurezza consigliate, come descritto in [Configurare la connettività SSL nel database di Azure per MySQL](concepts-ssl-connection-security.md).

Non è necessario toomove l'importazione e percorso di cloud speciali tooany i file di esportazione durante la migrazione di Database tooAzure per MySQL. 

## <a name="create-a-database-on-hello-azure-database-for-mysql-server"></a>Creare un database in hello Azure Database per il server MySQL
Creare un database vuoto in hello Azure Database di MySQL server in cui i dati di hello toomigrate. Utilizzare uno strumento come database di hello toocreate Workbench di MySQL, Toad o Navicat. database di Hello può avere hello stesso nome come database hello contenente dati hello dump oppure è possibile creare un database con un nome diverso.

tooget connessi, individuare informazioni di connessione hello hello **proprietà** riquadro nel Database di Azure per MySQL.

![Trovare le informazioni di connessione hello in hello portale di Azure](./media/concepts-migrate-import-export/1_server-properties-name-login.png)

Aggiungere tooMySQL informazioni di connessione hello Workbench.

![Stringa di connessione MySQL Workbench](./media/concepts-migrate-import-export/2_setup-new-connection.png)

## <a name="determine-when-toouse-import-and-export-techniques-instead-of-a-dump-and-restore"></a>Determinare quando toouse importare ed esportare tecniche anziché un dump e ripristino
Utilizzare tooimport strumenti MySQL ed esportare database nel Database di MySQL di Azure in hello seguenti scenari. In altri scenari, è possibile trarre vantaggio dall'utilizzo di hello [dump e il ripristino](concepts-migrate-dump-restore.md) approccio invece. 

- Quando è necessario tooselectively scegliere alcuni tooimport tabelle da un database MySQL esistente nel Database di MySQL di Azure, la migliore toouse hello importazione ed esportazione tecnica.  In questo modo, è possibile omettere tutte le tabelle non necessari dai tempi toosave hello e alle risorse. Ad esempio, utilizzare hello `--include-tables` o `--exclude-tables` con [mysqlpump](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html#option_mysqlpump_include-tables) hello e `--tables` con [mysqldump](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html#option_mysqldump_tables).
- Quando si spostano gli oggetti di database hello diversi dalle tabelle, crearli in modo esplicito. Includono vincoli (chiave primaria, chiave esterna, indici), viste, funzioni, procedure, trigger e gli oggetti di qualsiasi altro database che si desidera toomigrate.
- Quando si esegue la migrazione di dati da origini dati esterne diverse da un database MySQL, creare un file flat e importarli usando [mysqlimport](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html).

Assicurarsi che tutte le tabelle nel database di hello usano il motore di archiviazione InnoDB hello quando si carica dati nel Database di Azure per MySQL. Il Database di Azure per MySQL supporta solo hello InnoDB motore di archiviazione, quindi non supporta i motori di archiviazione alternativo. Se le tabelle richiedono motori di archiviazione alternativo, tooconvert assicurarsi di essere in formato di toouse hello InnoDB engine prima hello migrazione tooAzure Database MySQL. 

Ad esempio, se si dispone di un'app web o WordPress che usa il motore di MyISAM hello, innanzitutto convertire hello tabelle per la migrazione dei dati di hello in tabelle InnoDB. Ripristinare quindi tooAzure Database di MySQL. Clausola hello utilizzare `ENGINE=INNODB` tooset hello motore per la creazione di una tabella e quindi si trasferiscono dati hello in tabella compatibile di hello prima della migrazione hello. 

   ```sql
   INSERT INTO innodb_table SELECT * FROM myisam_table ORDER BY primary_key_columns
   ```

## <a name="performance-recommendations-for-import-and-export"></a>Consigli relativi alle prestazioni per l'importazione ed esportazione
-   Creare indici cluster e chiavi primarie prima di caricare dati. Caricare i dati nell'ordine delle chiavi primarie. 
-   Ritardare la creazione di indici secondari fino al termine del caricamento dei dati. Creare tutti gli indici secondari dopo il caricamento. 
-   Disabilitare i vincoli di chiave esterna prima del caricamento. La disabilitazione dei controlli della chiave esterna offre miglioramenti significativi delle prestazioni. Abilitare i vincoli hello e verificare dati hello dopo hello carico tooensure integrità referenziale.
-   Caricare i dati in parallelo. Evitare una quantità eccessiva parallelismo causare toohit un limite di risorse e monitorare le risorse con le metriche hello disponibili nel portale di Azure hello. 
-   Usare le tabelle partizionate quando appropriato.

## <a name="import-and-export-by-using-mysql-workbench"></a>Importare ed esportare con MySQL Workbench
Esistono due modi tooexport e l'importazione di dati nell'area di lavoro di MySQL. ognuno destinato a uno scopo diverso. 

### <a name="table-data-export-and-import-wizards-from-hello-object-browsers-context-menu"></a>Dati della tabella esportare e importare le procedure guidate dal menu di scelta rapida hello del Visualizzatore
![Procedure guidate Workbench di MySQL nel menu di scelta rapida hello del Visualizzatore](./media/concepts-migrate-import-export/p1.png)

procedure guidate di Hello per dati della tabella supportano l'importazione e operazioni di esportazione utilizzando i file CSV e JSON. Includono diverse opzioni di configurazione, ad esempio separatori, selezione colonne e selezione di codifica. È possibile eseguire ogni procedura guidata su server MySQL connessi in modalità remota o locale. azione di importazione Hello include tabelle, colonne e i mapping dei tipi. 

È possibile accedere a queste procedure guidate dal menu di scelta rapida del Visualizzatore oggetti hello facendo clic su una tabella. Scegliere quindi **Table Data Export Wizard** (Esportazione guidata di tabelle) o **Table Data Import Wizard** (Importazione guidata di tabelle). 

#### <a name="table-data-export-wizard"></a>Esportazione guidata di tabelle
Hello esempio seguente Esporta file CSV di hello tabella tooa: 
1. Fare clic sulla tabella hello toobe database hello esportata. 
2. Selezionare **Table Data Export Wizard** (Esportazione guidata di tabelle). Selezionare toobe colonne hello esportata, offset di riga (se presente) e count (se presente). 
3. In hello **selezionare i dati per l'esportazione** pagina, fare clic su **Avanti**. Selezionare il percorso di file hello, CSV o JSON il tipo di file. Selezionare inoltre separatore di riga hello, metodo di inclusione, stringhe e il separatore di campo. 
4. In hello **percorso di file di output selezionare** pagina, fare clic su **Avanti**. 
5. In hello **esportare dati** pagina, fare clic su **Avanti**.

#### <a name="table-data-import-wizard"></a>Importazione guidata di tabelle
Hello esempio seguente importa hello tabella da un file CSV:
1. Fare clic sulla tabella hello di hello database toobe importati. 
2. Sfoglia tooand selezionare hello toobe file CSV importati e quindi fare clic su **Avanti**. 
3. Selezionare una tabella di destinazione hello (nuova o esistente) e seleziona o deselezionare hello **istruzione Truncate table prima dell'importazione** casella di controllo. Fare clic su **Avanti**.
4. Selezionare la codifica e hello toobe colonne importate e quindi fare clic su **Avanti**. 
5. In hello **importare dati** pagina, fare clic su **Avanti**. Hello importazione hello dei dati di conseguenza.

### <a name="sql-data-export-and-import-wizards-from-hello-navigator-pane"></a>Dati SQL esportazione e importazione di procedure guidate dal Pannello di navigazione hello
Utilizzare una procedura guidata tooexport o importare SQL generato dal Workbench di MySQL o generato dal comando mysqldump hello. Accedere a queste procedure guidate da hello **Navigator** riquadro oppure selezionando **Server** dal menu principale di hello. Selezionare quindi **Esporta dati** o **Importa dati**. 

#### <a name="data-export"></a>Esportazione dati
![Esportazione di dati di MySQL Workbench utilizzando il pannello di navigazione hello](./media/concepts-migrate-import-export/p2.png)

È possibile utilizzare hello **esportazione dati** scheda tooexport i dati di MySQL. 
1. Selezionare ogni schema che si desidera tooexport, se lo si desidera scegliere oggetti specifici dello schema e alle tabelle da ogni schema e genera esportazione hello. Opzioni di configurazione includono esportazione tooa cartella del progetto o file SQL autonomo, eseguire il dump degli eventi e routine stored o ignorare i dati della tabella. 
 
   In alternativa, utilizzare **esportare un Set di risultati** tooexport un risultato specifico impostato in hello SQL editor tooanother formato, ad esempio CSV, JSON, HTML e XML. 
3. Selezionare tooexport gli oggetti di database hello e configurare hello relative opzioni.
4. Fare clic su **aggiornamento** oggetti di tooload hello corrente.
5. Facoltativamente, aprire hello **opzioni avanzate** scheda toorefine l'operazione di esportazione hello. Ad esempio, aggiungere blocchi di tabella, usare istruzioni "replace" anziché "insert" e segnalare gli identificatori con l'apice inverso.
6. Fare clic su **avviare esportare** toobegin processo di esportazione hello.


#### <a name="data-import"></a>Importazione dati
![Importazione di dati da MySQL Workbench tramite Management Navigator](./media/concepts-migrate-import-export/p3.png)

È possibile utilizzare hello **importazione dati** scheda tooimport o ripristinare i dati esportati dall'operazione di esportazione di dati hello o dal comando mysqldump hello. 
1. Scegliere la cartella di progetto hello o file SQL autonomo, scegliere tooimport schema hello in oppure **New** toodefine un nuovo schema. 
2. Fare clic su **avviare importazione** toobegin processo di importazione hello.

## <a name="next-steps"></a>Passaggi successivi
Per un altro approccio di migrazione, vedere [Eseguire la migrazione del database MySQL mediante dump e ripristino nel database di Azure per MySQL](concepts-migrate-dump-restore.md). 
