---
title: "dati di aaaLoad in Azure SQL Data Warehouse – Data Factory | Documenti Microsoft"
description: In questa esercitazione carica i dati in Azure SQL Data Warehouse utilizzando Data Factory di Azure e Usa un database di SQL Server come origine dati hello.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Caricare i dati in SQL Data Warehouse

È possibile utilizzare dati tooload Data Factory di Azure in Azure SQL Data Warehouse da qualsiasi hello [archivi dati di origine supportata](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Ad esempio, i dati possono essere caricati da un database SQL di Azure o da un database Oracle in SQL Data Warehouse tramite Data Factory. Esercitazione in questo articolo illustra come dati tooload da un Server SQL locale del database in un data warehouse SQL.

**Tempo stimato**: in questa esercitazione richiede circa 10-15 minuti toocomplete una volta soddisfatti i prerequisiti di hello.

## <a name="prerequisites"></a>Prerequisiti

- È necessario un **database di SQL Server** con le tabelle che contengono dati hello toobe copiate toohello data warehouse di SQL.  

- È necessario un **SQL Data Warehouse** online. Se si dispone già di un data warehouse, informazioni su come troppo[creare un Data Warehouse di SQL Azure](sql-data-warehouse-get-started-provision.md).

- È necessario un **account di archiviazione di Azure**. Se si dispone già di un account di archiviazione, informazioni su come troppo[creare un account di archiviazione](../storage/common/storage-create-storage-account.md). Per prestazioni ottimali, individuare l'account di archiviazione hello e hello data warehouse in hello stessa regione di Azure.

## <a name="configure-a-data-factory"></a>Configurare una data factory
1. Accedi toohello [portale di Azure][].
2. Individuare il data warehouse e fare clic su tooopen è.
3. Nel pannello principale hello, fare clic su **Carica dati** > **Azure Data Factory**.

    ![Avviare la procedura guidata di caricamento dei dati](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Se si ha una data factory nella sottoscrizione di Azure, viene visualizzato un **nuova Data Factory** la finestra di dialogo in una scheda separata del browser hello. Compilare hello informazioni richieste e fare clic su **crea**. Dopo la creazione di data factory di hello hello **nuova Data Factory** chiude la finestra di dialogo e viene visualizzato hello **selezionare Data Factory** la finestra di dialogo.

    Se si dispone di uno o più factory di dati già presenti nella sottoscrizione di Azure hello, vedrai hello **selezionare Data Factory** la finestra di dialogo. Nella finestra di dialogo, è possibile selezionare una data factory esistente o fare clic su **Crea nuova data factory** toocreate uno nuovo.

    ![Configurare una data factory](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. In hello **selezionare Data Factory** della finestra di dialogo hello **caricare dati** opzione è selezionata per impostazione predefinita. Fare clic su **Avanti** toostart la creazione di un'attività di caricamento di dati.

## <a name="configure-hello-data-factory-properties"></a>Configurare le proprietà di hello data factory
Dopo avere creato una data factory, hello sarà dati hello tooconfigure durante il caricamento di pianificazione.

1. Per **Nome attività** immettere **DWLoadData-fromSQLServer**.
2. Utilizzare hello predefinito **Esegui una volta** opzione, fare clic su **Avanti**.

    ![Configurare il bilanciamento del carico](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Configurare l'archivio dati di origine hello e gateway
Ora informare Data Factory di database di SQL Server on-premise hello da cui si desidera dati tooload.

1. Scegliere **SQL Server** dai dati di origine supportato di hello archiviare catalogo e fare clic su **Avanti**.

    ![Scegliere l'origine SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. Oggetto **database di SQL Server on-premise hello specificare** viene visualizzata la finestra. prima di Hello **nome connessione** campo viene automaticamente compilato. secondo campo Hello chiede nome hello di hello **Gateway**. Se si utilizza una data factory esistente che dispone già di un gateway, è possibile riutilizzare gateway hello selezionandolo dall'elenco a discesa hello. Fare clic su hello **crea Gateway** collegamento toocreate un Gateway di gestione di dati.  

    > [!NOTE]
    > Se l'archivio dati di origine hello è locale o in una macchina virtuale IaaS di Azure, è necessario un Gateway di gestione di dati. Un gateway ha una relazione 1-1 con una data factory. Non può essere utilizzato da un altro data factory, ma può essere utilizzato da più attività con hello di caricamento di dati stessa data factory. Un gateway può essere utilizzato tooconnect toomultiple gli archivi dati durante l'esecuzione di attività di caricamento dei dati.
    >
    > Per informazioni dettagliate sul gateway hello, vedere [Gateway di gestione dati](../data-factory/data-factory-data-management-gateway.md) articolo.

3. Verrà visualizzata la finestra di dialogo **Crea gateway**. Come nome immettere **GatewayForDWLoading** e fare clic su **Crea**.

4. Verrà visualizzata la finestra di dialogo **Configure Gateway** (Configura gateway). Fare clic su **avviare l'installazione rapida in questo computer** tooautomatically scaricare, installare e registrare il Gateway di gestione di dati sul computer corrente. stato di Hello è visualizzato in una finestra popup. Se la macchina hello non può connettersi archivio dati toohello, è possibile eseguire manualmente [scaricare e installare il gateway hello](https://www.microsoft.com/download/details.aspx?id=39717) in un computer che può connettersi a dati toohello archiviare e quindi utilizzare tooregister chiave hello.
    > [!NOTE]
    > l'installazione rapida Hello funziona in modo nativo con Microsoft Edge e Internet Explorer. Se si utilizza Google Chrome, installare innanzitutto estensione ClickOnce hello dall'archivio web Chrome.

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Attendere toocomplete il programma di installazione di gateway hello. Una volta gateway hello viene registrata correttamente e sia in linea, chiude la finestra popup di hello e nuovo gateway hello viene visualizzato nel campo gateway hello. Quindi, compilare il resto di hello richiesto campi come indicato di seguito, quindi fare clic su **Avanti**.
    - **Nome del server**: nome di hello SQL Server locale.
    - **Nome del database**: database SQL Server.
    - **Crittografia delle credenziali**: hello predefinito "dal web browser".
    - **Tipo di autenticazione**: scegliere il tipo di hello di autenticazione si sta usando.
    - **Nome utente** e **password**: immettere il nome di utente hello e una password per un utente che dispone di dati di autorizzazione toocopy hello.

    ![Avviare l'installazione rapida](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. passaggio successivo Hello è tabelle hello toochoose da cui toocopy hello. È possibile filtrare le tabelle di hello utilizzando le parole chiave. Ed è possibile visualizzare l'anteprima dello schema di dati e tabella hello nel pannello inferiore hello. Dopo aver completato la selezione, fare clic su **Avanti**.

    ![Selezionare le tabelle](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Configurare destinazione hello, il Data Warehouse SQL

Ora informare Data Factory di informazioni sulla destinazione hello.

1. Le informazioni di connessione di SQL Data Warehouse sono inserite automaticamente. Immettere la password di hello per nome utente hello. e fare clic su **Avanti**.

    ![Configurare la destinazione](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Viene visualizzato un mapping di tabella intelligente che esegue il mapping di tabelle di origine toodestination in base ai nomi di tabella. Se la tabella hello non esiste nella destinazione hello, per impostazione predefinita ADF verrà creato uno con hello stesso nome (si applica tooSQL Server o Database SQL di Azure come origine). È anche possibile scegliere toomap tooan esistente nella tabella. Controllare le associazioni e fare clic su **Avanti**.

    ![Eseguire il mapping delle tabelle](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Esaminare il mapping dello schema hello e cercare i messaggi di errore o avviso. Il mapping intelligente è basato sui nomi delle colonne. Se è presente una conversione di tipo di dati non supportati tra colonne di origine e destinazione hello, viene visualizzato un messaggio di errore insieme tabella corrispondente hello. Se si sceglie automaticamente Data Factory toolet creare tabelle hello, conversione di tipi di dati appropriati può verificarsi se necessario incompatibilità hello toofix tra gli archivi di origine e di destinazione.

    ![Eseguire il mapping dello schema](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Fare clic su **Avanti**.

## <a name="configure-hello-performance-settings"></a>Configurare le impostazioni delle prestazioni di hello
Nelle configurazioni di prestazioni hello, configurare un account di archiviazione di Azure utilizzato per la gestione temporanea di dati hello prima viene caricato in SQL Data Warehouse rendere più efficiente utilizzando [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). Dopo l'operazione di copia hello, dati provvisorio hello nel servizio di archiviazione verranno eseguiti automaticamente la pulizia.

Selezionare un account di archiviazione di Azure esistente e fare clic su **Avanti**.

![Configurare il BLOB di gestione temporanea](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Esaminare le informazioni di riepilogo e distribuire la pipeline hello

Rivedere la configurazione di hello e fare clic su **fine** pipeline hello toodeploy di pulsante.

![Distribuire la data factory](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Monitorare lo stato di avanzamento del caricamento dei dati

È possibile visualizzare l'avanzamento della distribuzione hello e i risultati in hello **distribuzione** pagina.

1. Una volta hello distribuzione viene eseguita, fare clic su collegamento hello **fare clic qui pipeline copia toomonitor** dati toomonitor avanzamento del caricamento.

    ![Monitorare la pipeline](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. Hello appena creato **DWLoadData fromSQLServer** pipeline per il caricamento dei dati viene automaticamente selezionato da sinistra hello **Esplora inventario risorse**.

    ![Visualizzare la pipeline](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Fare clic su nella pipeline hello centro hello hello toosee pannello stato dettagliato per ogni tabella in cui viene eseguito il mapping tooan attività.

    ![Visualizzare l'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Scegliere ulteriormente in un'attività e visualizzare dati hello il caricamento dei dettagli nel riquadro di destra hello tra dimensioni dei dati, le righe, velocità effettiva e così via.

    ![Visualizzare i dettagli dell'attività della tabella](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. Fare clic su questo monitoraggio visualizzazione versioni successive, visitare tooyour SQL Data Warehouse, toolaunch **Load Data > Data Factory di Azure**, selezionare l'ambiente di produzione e scegliere **monitorare esistente durante il caricamento di attività**.

## <a name="next-steps"></a>Passaggi successivi

vedere il tooSQL database Data Warehouse, toomigrate [Cenni preliminari sulla migrazione](sql-data-warehouse-overview-migrate.md).

toolearn ulteriori informazioni su Azure Data Factory e le funzionalità di spostamento dei dati, vedere hello seguenti articoli:

- [Introduzione tooAzure Data Factory](../data-factory/data-factory-introduction.md)
- [Spostare dati con l'attività di copia](../data-factory/data-factory-data-movement-activities.md)
- [Spostare dati tooand da usando Azure Data Factory di Azure SQL Data Warehouse](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

vedere i dati in SQL Data Warehouse, tooexplore hello seguenti articoli:

- [Connettersi tooSQL Data Warehouse con Visual Studio e SSDT](sql-data-warehouse-query-visual-studio.md)
- [Visualizzare i dati con Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)

<!-- Azure references -->
[portale di Azure]: https://portal.azure.com
