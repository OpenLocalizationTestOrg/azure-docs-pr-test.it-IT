---
title: dati aaaLoad da SQL Server in Azure SQL Data Warehouse (SSIS) | Documenti Microsoft
description: Viene illustrato come toocreate dati toomove di un pacchetto di SQL Server Integration Services (SSIS) da una vasta gamma di dati origini tooSQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e2c252e9-0828-47c2-a808-e3bea46c134a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/30/2017
ms.author: cakarst;douglasl;barbkess
ms.openlocfilehash: bb28a08807a5b07832b85f2f074c2acf912c1dc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-ssis"></a>Caricare dati da SQL Server in Azure SQL Data Warehouse (SSIS)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Creare dati tooload di un pacchetto di SQL Server Integration Services (SSIS) da SQL Server in Azure SQL Data Warehouse. È facoltativamente possibile ristrutturare, trasformare e pulire i dati di hello durante il passaggio attraverso il flusso di dati SSIS hello.

In questa esercitazione si apprenderà come:

* Creare un nuovo progetto di Integration Services in Visual Studio.
* Connettersi toodata origini, tra cui SQL Server (come origine) e SQL Data Warehouse (come una destinazione).
* Progettare un pacchetto SSIS che carica i dati dall'origine hello in destinazione hello.
* Esecuzione hello dati hello tooload del pacchetto SSIS.

In questa esercitazione Usa SQL Server come origine dati hello. SQL Server può essere eseguito in locale o in una macchina virtuale di Azure.

## <a name="basic-concepts"></a>Concetti di base
pacchetto di Hello è hello unità di lavoro di SSIS. I pacchetti correlati sono raggruppati in progetti. Progetti e pacchetti di progettazione vengono creati in Visual Studio con SQL Server Data Tools. progettazione di Hello processo è un processo di visual in cui si trascinano le componenti dall'area di progettazione toohello della casella degli strumenti hello, connetterle e impostare le relative proprietà. Dopo aver completato il pacchetto, è possibile facoltativamente distribuirlo tooSQL Server per la sicurezza, il monitoraggio e gestione completa.

## <a name="options-for-loading-data-with-ssis"></a>Opzioni di caricamento dei dati con SSIS
SQL Server Integration Services (SSIS) è un set di strumenti flessibile che offre un'ampia gamma di opzioni per la connessione e il caricamento dei dati in SQL Data Warehouse.

1. Utilizzare un tooSQL tooconnect di destinazione ADO.NET Data Warehouse. Questa esercitazione viene utilizzato un componente di destinazione ADO.NET perché contiene hello minor numero di opzioni di configurazione.
2. Utilizzare un tooSQL tooconnect destinazione OLE DB Data Warehouse. Questa opzione può fornire prestazioni leggermente migliori rispetto a hello destinazione ADO.NET.
3. Utilizzare hello attività di caricamento Blob di Azure toostage hello dati nell'archiviazione Blob di Azure. Utilizzare quindi toolaunch di attività Esegui SQL SSIS hello uno script di Polybase che carica i dati di hello in SQL Data Warehouse. Questa opzione offre prestazioni ottimali di hello hello tre opzioni disponibili elencate di seguito. hello tooget attività di caricamento Blob di Azure, scaricare hello [Microsoft SQL Server 2016 Integration Services Feature Pack per Azure][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]. toolearn ulteriori informazioni su Polybase, vedere [Guida a PolyBase][PolyBase Guide].

## <a name="before-you-start"></a>Prima di iniziare
toostep di questa esercitazione, è necessario:

1. **SQL Server Integration Services (SSIS)**. SSIS è un componente di SQL Server e richiede una versione di valutazione o una versione con licenza di SQL Server. tooget una versione di valutazione di SQL Server 2016 Preview, vedere [SQL Server valutazioni][SQL Server Evaluations].
2. **Visual Studio** tooget hello disponibile Visual Studio Community Edition, vedere [Visual Studio Community][Visual Studio Community].
3. **SQL Server Data Tools per Visual Studio (SSDT)**. tooget SQL Server Data Tools per Visual Studio, vedere [SQL Download di Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)].
4. **Dati di esempio**. Questa esercitazione Usa i dati di esempio archiviati in SQL Server nel database di esempio AdventureWorks hello come hello toobe di dati di origine caricato in SQL Data Warehouse. hello tooget database di esempio AdventureWorks, vedere [database di esempio AdventureWorks 2014][AdventureWorks 2014 Sample Databases].
5. **Database di SQL Data Warehouse e relative autorizzazioni**. In questa esercitazione si connette tooa istanza di SQL Data Warehouse e carica i dati. È necessario toohave autorizzazioni toocreate una tabella e tooload dati.
6. **Regola del firewall**. Hai toocreate una regola del firewall in SQL Data Warehouse con l'indirizzo IP di hello del computer locale prima di poter caricare dati toohello SQL Data Warehouse.

## <a name="step-1-create-a-new-integration-services-project"></a>Passaggio 1: Creare un nuovo progetto di Integration Services
1. Avviare Visual Studio.
2. In hello **File** dal menu **New | Progetto**.
3. Passare toohello **installato | I modelli | Business Intelligence | Integration Services** tipi di progetto.
4. Selezionare **Progetto di Integration Services**. Specificare i valori per **Nome** e **Percorso** e quindi scegliere **OK**.

Visual Studio viene aperto e crea un nuovo progetto di Integration Services (SSIS). Visual Studio apre quindi progettazione hello per hello singolo nuovo pacchetto SSIS (package. dtsx) nel progetto hello. Vedrai hello seguenti aree dello schermo:

* A sinistra di hello, hello **della casella degli strumenti** componenti SSIS.
* Centro hello hello area di progettazione, con più schede. In genere si usa almeno hello **flusso di controllo** hello e **del flusso di dati** schede.
* In hello destra, hello **Esplora** hello e **proprietà** riquadri.
  
    ![][01]

## <a name="step-2-create-hello-basic-data-flow"></a>Passaggio 2: Creare il flusso di dati di base hello
1. Trascinare un'attività flusso di dati dall'area di toohello hello della casella degli strumenti dell'area di progettazione hello (su hello **flusso di controllo** scheda).
   
    ![][02]
2. Fare doppio clic sulla scheda flusso di dati tooswitch toohello di hello attività flusso di dati.
3. Dall'elenco di altre origini hello in hello della casella degli strumenti, trascinare un'area di progettazione toohello origine ADO.NET. Con l'adattatore di origine hello ancora selezionato, modificarne il nome troppo**origine SQL Server** in hello **proprietà** riquadro.
4. Dall'elenco di altre destinazioni hello in hello della casella degli strumenti, trascinare un'area di progettazione di destinazione ADO.NET toohello in hello origine ADO.NET. Con l'adattatore di destinazione hello ancora selezionato, modificarne il nome troppo**destinazione SQL DW** in hello **proprietà** riquadro.
   
    ![][09]

## <a name="step-3-configure-hello-source-adapter"></a>Passaggio 3: Configurare l'adattatore di origine hello
1. Fare doppio clic su hello di hello origine adapter tooopen **Editor origine ADO.NET**.
   
    ![][03]
2. In hello **Connection Manager** scheda di hello **Editor origine ADO.NET**, fare clic su hello **New** pulsante Avanti toohello **gestione connessione ADO.NET**hello tooopen elenco **Configura gestione connessione ADO.NET** finestra di dialogo e creare le impostazioni di connessione per il database di SQL Server hello carica i dati da cui questa esercitazione.
   
    ![][04]
3. In hello **Configura gestione connessione ADO.NET** finestra di dialogo fare clic su hello **New** hello tooopen pulsante **Connection Manager** finestra di dialogo e creare una nuova connessione dati.
   
    ![][05]
4. In hello **Connection Manager** finestra di dialogo casella, hello seguenti operazioni.
   
   1. Per **Provider**, selezionare hello SqlClient Data Provider.
   2. Per **nome Server**, immettere il nome di SQL Server hello.
   3. In hello **Log toohello server** selezionare o immettere le informazioni di autenticazione.
   4. In hello **Connetti tooa database** , selezionare il database di esempio AdventureWorks hello.
   5. Fare clic su **Test connessione**.
      
       ![][06]
   6. Nella finestra di dialogo hello che contiene i risultati di hello di test della connessione hello, fare clic su **OK** tooreturn toohello **Connection Manager** la finestra di dialogo.
   7. In hello **Connection Manager** la finestra di dialogo, fare clic su **OK** tooreturn toohello **Configura gestione connessione ADO.NET** la finestra di dialogo.
5. In hello **Configura gestione connessione ADO.NET** la finestra di dialogo, fare clic su **OK** tooreturn toohello **Editor origine ADO.NET**.
6. In hello **Editor origine ADO.NET**, in hello **nome della tabella hello o della vista hello** elenco, seleziona hello **Sales. SalesOrderDetail** tabella.
   
    ![][07]
7. Fare clic su **anteprima** toosee hello prime 200 righe di dati nella tabella di origine hello in hello **anteprima risultati Query** la finestra di dialogo.
   
    ![][08]
8. In hello **anteprima risultati Query** la finestra di dialogo, fare clic su **Chiudi** tooreturn toohello **Editor origine ADO.NET**.
9. In hello **Editor origine ADO.NET**, fare clic su **OK** toofinish configurazione dell'origine dati hello.

## <a name="step-4-connect-hello-source-adapter-toohello-destination-adapter"></a>Passaggio 4: Connettere hello origine toohello destinazione adattatore
1. Selezionare l'adattatore di origine hello nell'area di progettazione hello.
2. Fare clic su freccia hello blu che si estende dall'adattatore di origine hello e trascinarlo editor destinazione toohello fino al completo inserimento.
   
    ![][10]
   
    In un pacchetto SSIS tipico, utilizzare una serie di altri componenti dalla casella degli strumenti SSIS di hello tra origine hello e hello destinazione toorestructure, trasformazione e pulire i dati durante il passaggio attraverso il flusso di dati SSIS hello. tookeep più semplice possibile in questo esempio, ci si sta connettendo hello origine direttamente toohello destinazione.

## <a name="step-5-configure-hello-destination-adapter"></a>Passaggio 5: Configurare l'adattatore di destinazione hello
1. Fare doppio clic su hello di hello destinazione adapter tooopen **Editor destinazione ADO.NET**.
   
    ![][11]
2. In hello **Connection Manager** scheda di hello **Editor destinazione ADO.NET**, fare clic su hello **New** pulsante Avanti toohello **Connection manager**hello tooopen elenco **Configura gestione connessione ADO.NET** finestra di dialogo e creare impostazioni di connessione per il database di Azure SQL Data Warehouse hello carica i dati in cui questa esercitazione.
3. In hello **Configura gestione connessione ADO.NET** finestra di dialogo fare clic su hello **New** hello tooopen pulsante **Connection Manager** finestra di dialogo e creare una nuova connessione dati.
4. In hello **Connection Manager** finestra di dialogo casella, hello seguenti operazioni.
   1. Per **Provider**, selezionare hello SqlClient Data Provider.
   2. Per **nome Server**, immettere il nome di SQL Data Warehouse hello.
   3. In hello **Log toohello server** selezionare **utilizzare l'autenticazione di SQL** e immettere le informazioni di autenticazione.
   4. In hello **Connetti tooa database** , selezionare un database esistente di SQL Data Warehouse.
   5. Fare clic su **Test connessione**.
   6. Nella finestra di dialogo hello che contiene i risultati di hello di test della connessione hello, fare clic su **OK** tooreturn toohello **Connection Manager** la finestra di dialogo.
   7. In hello **Connection Manager** la finestra di dialogo, fare clic su **OK** tooreturn toohello **Configura gestione connessione ADO.NET** la finestra di dialogo.
5. In hello **Configura gestione connessione ADO.NET** la finestra di dialogo, fare clic su **OK** tooreturn toohello **Editor destinazione ADO.NET**.
6. In hello **Editor destinazione ADO.NET**, fare clic su **New** toohello Avanti **utilizzare una tabella o vista** hello tooopen elenco **Create Table** la finestra di dialogo una nuova tabella di destinazione con un elenco di colonne corrispondente tabella di origine hello toocreate.
   
    ![][12a]
7. In hello **Create Table** finestra di dialogo casella, hello seguenti operazioni.
   
   1. Modificare il nome di hello della tabella di destinazione hello troppo**SalesOrderDetail**.
   2. Rimuovere hello **rowguid** colonna. Hello **uniqueidentifier** tipo di dati non è supportato in SQL Data Warehouse.
   3. Modificare il tipo di dati hello di hello **LineTotal** colonna troppo**money**. Hello **decimale** tipo di dati non è supportato in SQL Data Warehouse. Per informazioni sui tipi di dati supportati, vedere [CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)].
      
       ![][12b]
   4. Fare clic su **OK** toocreate hello tabella e restituire toohello **Editor destinazione ADO.NET**.
8. In hello **Editor destinazione ADO.NET**selezionare hello **mapping** scheda toosee come colonne nell'origine hello mappati toocolumns nella destinazione hello.
   
    ![][13]
9. Fare clic su **OK** toofinish configurazione dell'origine dati hello.

## <a name="step-6-run-hello-package-tooload-hello-data"></a>Passaggio 6: Eseguire hello pacchetto tooload hello dati
Pacchetto di esecuzione hello facendo hello **avviare** pulsante sulla barra degli strumenti hello o selezionando una delle hello **eseguire** opzioni hello **Debug** menu.

Come pacchetto hello inizia toorun, vedere attività tooindicate giallo rotante ruote, nonché il numero di hello di righe elaborate finora.

![][14]

Al termine dell'esecuzione pacchetto hello, si vedere segni di spunta verde tooindicate successo nonché hello numero totale di righe di dati caricati hello origine toohello di destinazione.

![][15]

Congratulazioni. Utilizzati dati di SQL Server Integration Services tooload correttamente in Azure SQL Data Warehouse.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sul flusso di dati SSIS hello. Iniziare da qui: [Flusso di dati][Data Flow].
* Informazioni su come toodebug e risolvere i problemi relativi a destra i pacchetti nell'ambiente di progettazione hello. Iniziare da qui: [Strumenti per la risoluzione dei problemi di sviluppo di pacchetti][Troubleshooting Tools for Package Development].
* Informazioni su come toodeploy il SSIS progetti e pacchetti tooIntegration tooanother o Server di servizi di posizione di archiviazione. Iniziare da qui: [Distribuzione di progetti e pacchetti][Deployment of Projects and Packages].

<!-- Image references -->
[01]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-designer-01.png
[02]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ssis-data-flow-task-02.png
[03]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-03.png
[04]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-manager-04.png
[05]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-connection-05.png
[06]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/test-connection-06.png
[07]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-source-07.png
[08]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/preview-data-08.png
[09]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/source-destination-09.png
[10]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/connect-source-destination-10.png
[11]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/ado-net-destination-11.png
[12a]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-before-12a.png
[12b]: ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/destination-query-after-12b.png
[13]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/column-mapping-13.png
[14]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-running-14.png
[15]:  ./media/sql-data-warehouse-load-from-sql-server-with-integration-services/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: https://msdn.microsoft.com/library/mt143171.aspx
[Download SQL Server Data Tools (SSDT)]: https://msdn.microsoft.com/library/mt204009.aspx
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: https://msdn.microsoft.com/library/mt203953.aspx
[Data Flow]: https://msdn.microsoft.com/library/ms140080.aspx
[Troubleshooting Tools for Package Development]: https://msdn.microsoft.com/library/ms137625.aspx
[Deployment of Projects and Packages]: https://msdn.microsoft.com/library/hh213290.aspx

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://msftdbprodsamples.codeplex.com/releases/view/125550
