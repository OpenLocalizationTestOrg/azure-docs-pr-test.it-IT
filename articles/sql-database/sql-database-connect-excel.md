---
title: aaaConnect Excel tooSQL Database | Documenti Microsoft
description: Informazioni su come Microsoft Excel di tooconnect tooAzure SQL database nel cloud hello. Importare i dati in Excel per creare report ed esplorare i dati.
services: sql-database
keywords: connettere excel toosql, importare dati tooexcel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>La connessione a database SQL di Azure tooan di Excel e creare un report

La connessione a Excel tooa SQL database nel cloud hello e importare i dati e creare tabelle e grafici in base ai valori nel database di hello. In questa esercitazione che si imposterà connessione hello tra Excel e una tabella di database, salvare il file hello che archivia le informazioni di connessione dati e hello per Excel e quindi creare un grafico pivot da hello i valori del database.

Per iniziare, è necessario un database SQL in Azure. Se non si dispone di uno, vedere [creare il primo database SQL](sql-database-get-started-portal.md) tooget un database con dati di esempio attivo e in esecuzione in pochi minuti. Questo articolo descrive come importare i dati di esempio in Excel, ma è anche possibile seguire la procedura con dati personalizzati.

Sarà necessaria anche una copia di Excel. In questa esercitazione viene usato [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>La connessione a database SQL tooa di Excel e creare un file odc
1. tooconnect Excel tooSQL aprire Excel e quindi creare una nuova cartella di lavoro o aprire una cartella di lavoro di Excel esistente.
2. Nella barra dei menu hello nella parte superiore di hello di hello pagina fare clic su **dati**, fare clic su **da altre origini**, quindi fare clic su **da SQL Server**.
   
   ![Seleziona l'origine dati: la connessione a database tooSQL Excel.](./media/sql-database-connect-excel/excel_data_source.png)
   
   verrà visualizzata la finestra di Hello connessione guidata dati.
3. In hello **connettersi tooDatabase Server** hello tipo Database SQL nella finestra di dialogo **nome Server** tooconnect tooin hello modulo <*servername* > **. database.windows.net**. Ad esempio, **adworkserver.database.windows.net**.
4. In **credenziali di accesso**, fare clic su **hello utilizzare seguito nome utente e Password**, hello tipo **nome utente** e **Password** è impostato su Hello server di Database SQL quando viene creato e quindi fare clic su **Avanti**.
   
   ![Digitare le credenziali di nome e l'account di accesso server hello](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > A seconda dell'ambiente di rete, potrebbe non essere in grado di tooconnect o connessione hello vadano perduti se il server di Database SQL di hello non consentire il traffico verso l'indirizzo IP client. Passare toohello [portale di Azure](https://portal.azure.com/), fare clic su SQL Server, fare clic sul server, scegliere le impostazioni di firewall e aggiungere l'indirizzo IP client. Vedere [come impostazioni del firewall tooconfigure](sql-database-configure-firewall-settings.md) per informazioni dettagliate.
   > 
   > 
5. In hello **seleziona Database e tabella** finestra di dialogo, database selezionare hello desidera toowork con elenco hello e quindi fare clic su tabelle hello o viste che si desidera toowork con (è stato scelto **vGetAllCategories**), quindi Fare clic su **Avanti**.
   
    ![Selezionare un database e una tabella.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Hello **Salva File di connessione dati e di fine** viene visualizzata la finestra di dialogo, in cui immettere informazioni la file hello Office database connection (*. odc) utilizzato da Excel. È possibile lasciare le impostazioni predefinite hello o personalizzare le selezioni.
6. È possibile lasciare le impostazioni predefinite hello, ma hello nota **nome File** in particolare. A **descrizione**, **nome descrittivo**, e **parole** consentono e ricordare di altri utenti si connette tooand trovare la connessione di hello. Fare clic su **toouse prova sempre dati del file toorefresh** se si desiderano che le informazioni di connessione archiviate in file con estensione odc hello in modo che può aggiornare quando connette tooit e quindi fare clic su **fine**.
   
    ![Salvataggio di un file ODC](./media/sql-database-connect-excel/save-odc-file.png)
   
    Hello **importare dati** viene visualizzata la finestra di dialogo.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importare dati hello in Excel e creare un grafico pivot
Hai stabilita connessione hello e file hello creato con le informazioni di connessione e i dati, si sta leggendo dati hello tooimport.

1. In hello **l'importazione dei dati** finestra di dialogo, fare clic su hello desiderato per presentare i dati nel foglio di lavoro hello e quindi fare clic su **OK**. In questo caso è stato scelto **Grafico pivot**. È anche possibile scegliere toocreate un **nuovo foglio di lavoro** o troppo**aggiungere questo modello di dati di tooa dati**. Per altre informazioni sui modelli di dati, vedere [Creare un modello di dati in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Fare clic su **proprietà** tooexplore informazioni file odc hello è stato creato in hello precedente passaggio e toochoose opzioni per l'aggiornamento dati hello.
   
    ![Scelta di hello formato per i dati in Excel](./media/sql-database-connect-excel/import-data.png)
   
    foglio di lavoro Hello dispone ora di un grafico e una tabella pivot vuota.
2. In **PivotTable Fields**, selezionare tutti hello caselle di controllo per hello campi che si desidera tooview.
   
    ![Configurare un report di database.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Se si desidera tooconnect altri database toohello cartelle di lavoro e fogli di lavoro di Excel, fare clic su **dati**, fare clic su **connessioni**, fare clic su **Aggiungi**, scegliere connessione hello è stato creato elenco di hello e quindi fare clic su **aprire**.
> ![Aprire una connessione da un'altra cartella di lavoro](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[connettersi tooSQL Database con SQL Server Management Studio](sql-database-connect-query-ssms.md) avanzati di analisi e l'esecuzione di query.
* Informazioni sui vantaggi hello [pool elastici](sql-database-elastic-pool.md).
* Informazioni su come troppo[creare un'applicazione web che si connette tooSQL Database back-end hello](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

