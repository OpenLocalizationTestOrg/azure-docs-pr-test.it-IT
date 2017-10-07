---
title: aaaVisualize dati di SQL Data Warehouse con Microsoft Azure di Power BI
description: Visualizzare i dati di SQL Data Warehouse con Power BI
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Visualizzare i dati con Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

In questa esercitazione illustra come toouse Power BI tooconnect tooSQL Data Warehouse e creare alcune visualizzazioni di base.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toostep di questa esercitazione, è necessario:

* Un Data Warehouse SQL precaricati con database AdventureWorksDW hello. tooprovision questa operazione, vedere [creare un Data Warehouse SQL] [ Create a SQL Data Warehouse] e selezionare i dati di esempio hello tooload. Se si ha già un data warehouse, ma non i dati di esempio, è possibile [caricare manualmente i dati di esempio][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. La connessione a database tooyour
tooopen Power BI e connettersi a database AdventureWorksDW tooyour:

1. Sign in hello [portale di Azure][Azure portal].
2. Fare clic su **Database SQL** e scegliere il database SQL Data Warehouse AdventureWorks.
   
    ![Trovare il database][1]
3. Fare clic su pulsante 'Apri in Power BI' hello.
   
    ![Pulsante Power BI][2]
4. Dovrebbe essere pagina connessione di SQL Data Warehouse hello visualizzando l'indirizzo web di database. Fare clic su Avanti.
   
    ![Connessione a Power BI][3]
5. Immettere il nome utente del server SQL Azure e la password e sarà completamente connesso tooyour database di SQL Data Warehouse.
   
    ![Accesso a Power BI][4]
6. Dopo l'accesso a Power BI, fare clic su set di dati AdventureWorksDW hello nel pannello sinistro hello. Verrà aperto il database di hello.
   
    ![Apertura di AdventureWorksDW in Power BI][5]

## <a name="2-create-a-report"></a>2. Creare un report
Si è ora pronti toouse Power BI tooanalyze i dati di esempio AdventureWorksDW. analisi di hello tooperform, AdventureWorksDW dispone di una vista denominata AggregateSales. Questa vista contiene alcune metriche chiave di hello per l'analisi delle vendite hello della società hello.

1. toocreate una mappa dell'importo delle vendite in base a codice toopostal, nel riquadro di destra campi hello, fare clic su hello AggregateSales visualizzazione tooexpand è. Fare clic su tooselect di colonne PostalCode e SalesAmount hello li.
   
    ![Selezione di AggregateSales in Power BI][6]
   
    Power BI riconosce automaticamente tali informazioni come dati geografici e le inserisce direttamente in una mappa.
   
    ![Mappa di Power BI][7]
2. In questo passaggio viene creato un grafico a barre che mostra gli importi delle vendite per reddito del cliente. toocreate questo toohello passa espanso AggregateSales visualizzazione. Fare clic su campo SalesAmount hello. Trascinare hello reddito del cliente campo toohello sinistro e rilasciarlo nell'asse.
   
    ![Selezione asse in Power BI][8]
   
    Grafico a barre hello è stata spostata su hello sinistra.
   
    ![Barra di Power BI][9]
3. In questo passaggio viene creato un grafico a linee che mostra gli importi delle vendite per data dell'ordine. toocreate questo toohello passa espanso AggregateSales visualizzazione. Fare clic su SalesAmount e OrderDate. Nella colonna visualizzazioni hello fare clic sull'icona di grafico a linee di hello; si tratta prima icona hello nella seconda riga di hello in visualizzazioni.
   
    ![Selezione del grafico a linee in Power BI][10]
   
    Ora disponibile un report che mostra tre visualizzazioni diverse dei dati di hello.
   
    ![Riga di Power BI][11]

Per salvare lo stato in qualsiasi momento, fare clic su **File** e selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
Ora che ti forniamo alcuni toowarm ora con dati di esempio hello, vedere come troppo[sviluppare][develop], [caricare][load], o [ eseguire la migrazione][migrate]. O dare un'occhiata hello [sito Web di Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
