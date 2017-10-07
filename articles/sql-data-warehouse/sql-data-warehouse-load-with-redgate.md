---
title: aaaUse Redgate tooload dati tooyour Azure del data warehouse | Documenti Microsoft
description: Informazioni su come Studio di piattaforma di toouse Redgate dati per scenari di data warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a>Caricare dati con Data Platform Studio di Redgate
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

In questa esercitazione illustra come toouse [dati piattaforma Studio del Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) dati toomove (dp) da un tooAzure di SQL Server on-premise SQL Data Warehouse. Dati piattaforma Studio applica correzioni più appropriato per la compatibilità di hello e ottimizzazioni, pertanto dispone di hello più rapidamente tooget modo Introduzione a SQL Data Warehouse.

> [!NOTE]
> [Redgate](http://www.red-gate.com), partner Microsoft da lunga data, offre diversi strumenti di SQL Server. Questa funzionalità di Data Platform Studio è disponibile gratuitamente per uso sia commerciale che non commerciale.
> 
> 

## <a name="before-you-begin"></a>Prima di iniziare
### <a name="create-or-identify-resources"></a>Creare o identificare le risorse
Prima di iniziare questa esercitazione, è necessario toohave:

* **Database di SQL Server locale**: hello dati che si desidera tooimport tooSQL Data Warehouse deve toocome da un Server SQL locale (versione 2008R2 o versione successiva). Data Platform Studio non è in grado di importare direttamente dati da un database SQL di Azure o da file di testo.
* **Account di archiviazione Azure**: Studio piattaforma dati prepara i dati hello nell'archiviazione Blob di Azure prima di caricarli in SQL Data Warehouse. account di archiviazione Hello devono usare modello di distribuzione di "gestione di risorse" hello (impostazione predefinita hello) anziché il modello di distribuzione "Classiche" hello. Se non si dispone di un account di archiviazione, informazioni su come tooCreate un account di archiviazione. 
* **SQL Data Warehouse**: in questa esercitazione sposta dati hello da tooSQL di SQL Server on-premise Data Warehouse, pertanto è necessario toohave online a un data warehouse. Se si dispone già di un data warehouse, informazioni su come tooCreate un Data Warehouse di SQL Azure.

> [!NOTE]
> Le prestazioni sono migliori se l'account di archiviazione hello e hello data warehouse vengono creati in hello stessa area.
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a>Passaggio 1: Accedi tooData Studio piattaforma con l'account di Azure
Aprire il web browser e passare toohello [Studio piattaforma dati](https://www.dataplatformstudio.com/) sito Web. Accedi con hello stesso account di Azure che è usato toocreate hello storage account e del data warehouse. Se l'indirizzo di posta elettronica è associato sia un lavoro account e un account Microsoft, che account hello toochoose con tooyour di accedere alle risorse.

> [!NOTE]
> Se si tratta del primo utilizzo Studio piattaforma dati, sono frequenti toogrant hello applicazione autorizzazione toomanage le risorse di Azure.
> 
> 

## <a name="step-2-start-hello-import-wizard"></a>Passaggio 2: Avviare Importazione guidata hello
Dalla schermata principale di hello dei punti di distribuzione, selezionare hello importazione tooAzure SQL Data Warehouse collegamento toostart hello importazione guidata.

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a>Passaggio 3: Installare hello dati piattaforma Studio Gateway
database di SQL Server on-premise tooyour tooconnect, è necessario tooinstall hello Gateway dei punti di distribuzione. gateway Hello è un agente client che fornisce accesso tooyour ambiente locale, estrae i dati di hello e lo carica tooyour account di archiviazione. I dati non passano mai attraverso i server Redgate. hello tooinstall Gateway:

1. Fare clic su hello **crea Gateway** collegamento
2. Scaricare e installare il Gateway di hello con hello programma di installazione fornito

![][2]

> [!NOTE]
> Hello Gateway può essere installato in tutti i computer con database di SQL Server origine toohello accesso rete. Accede a database di SQL Server hello utilizzando l'autenticazione di Windows hello credenziali dell'utente corrente hello.
> 
> 

Una volta installato, hello tooConnected modifiche dello stato di Gateway ed è possibile fare clic su Avanti.

## <a name="step-4-identify-hello-source-database"></a>Passaggio 4: Identificare i database di origine hello
In hello *immettere nome Server* casella di testo, immettere il nome di hello del server di hello che ospita il database e selezionare **Avanti**. Quindi, dal menu a discesa hello, selezionare hello database tooimport dati.

![][3]

DP controlla se i database selezionati di hello per le tabelle tooimport. Per impostazione predefinita, dei punti di distribuzione consente di importare tutte le tabelle hello hello database. È possibile selezionare o deselezionare le tabelle espandendo hello tutte le tabelle di collegamento. Selezionare hello rollforward toomove di pulsante Avanti.

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a>Passaggio 5: Scegliere una data di archiviazione account toostage hello
Dei punti di distribuzione richiede i dati hello toostage un percorso. Scegliere un account di archiviazione esistente dalla sottoscrizione e selezionare **Next** (Avanti).

> [!NOTE]
> Crea un nuovo contenitore blob in hello scelto l'account di archiviazione e utilizzare una cartella distinta per ogni importazione dei punti di distribuzione.
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a>Passaggio 6: Selezionare un data warehouse
È quindi necessario selezionare un online [Azure SQL Data Warehouse](http://aka.ms/sqldw) dati hello tooimport nel database. Dopo aver selezionato il database, è necessario tooenter hello credenziali tooconnect toohello del database e selezionare **Avanti**.

![][5]

> [!NOTE]
> DP unisce le tabelle di dati di origine hello in data warehouse di hello. DP Avvisa se il nome di tabella hello richiede toooverwrite esistenti nelle tabelle hello data warehouse. È possibile eliminare tutti gli oggetti esistenti nel data warehouse di hello tracciando Elimina tutti gli oggetti esistenti prima dell'importazione.
> 
> 

## <a name="step-7-import-hello-data"></a>Passaggio 7: Importare dati hello
DP conferma che si desidera dati hello tooimport. Fare clic su hello inizio pulsante toobegin hello dati importazione.

![][6]

Dei punti di distribuzione consente di visualizzare una visualizzazione che mostra lo stato di avanzamento hello di estrazione e caricamento di dati hello dal hello locale di SQL Server e hello lo stato di avanzamento dell'importazione di hello in SQL Data Warehouse.

![][7]

Una volta completata l'importazione di hello, dei punti di distribuzione consente di visualizzare un riepilogo di importazione dei dati hello e un report delle modifiche di correzioni hello che sono state eseguite.

![][8]

## <a name="next-steps"></a>Passaggi successivi
tooexplore i dati all'interno di SQL Data Warehouse, avviare la visualizzazione:

* [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)] (Eseguire query in Azure SQL Data Warehouse (Visual Studio))
* [Visualizzare i dati con Power BI][Visualize data with Power BI]

altre informazioni sulle dati piattaforma Studio del Redgate toolearn:

* [Visitare la home page dei punti di distribuzione hello](http://www.dataplatformstudio.com/)
* [Guardare una demo di DPS su Channel9](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

Per una panoramica di altri modi toomigrate e caricare i dati in SQL Data Warehouse vedere:

* [Eseguire la migrazione del Data Warehouse di tooSQL soluzione][Migrate your solution tooSQL Data Warehouse]
* [Caricare i dati in Azure SQL Data Warehouse](sql-data-warehouse-overview-load.md)

Per ulteriori suggerimenti per lo sviluppo, vedere hello [Cenni preliminari sullo sviluppo di SQL Data Warehouse](sql-data-warehouse-overview-develop.md).

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
