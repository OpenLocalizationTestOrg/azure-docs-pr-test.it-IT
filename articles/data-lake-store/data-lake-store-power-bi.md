---
title: dati aaaAnalyze in archivio Data Lake tramite Power BI | Documenti Microsoft
description: Utilizzare i dati di Power BI tooanalyze archiviati nell'archivio Azure Data Lake
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Analizzare i dati in Archivio Data Lake con Power BI
In questo articolo si apprenderà come toouse tooanalyze di Power BI Desktop e visualizzare i dati archiviati nell'archivio Azure Data Lake.

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare questa esercitazione, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Account di Archivio Data Lake di Azure**. Seguire le istruzioni di hello in [introduzione archivio Azure Data Lake tramite il portale di Azure hello](data-lake-store-get-started-portal.md). Questo articolo si presuppone che è già stato creato un account archivio Data Lake, denominato **mybidatalakestore**e caricamento di un file di dati di esempio (**Drivers.txt**) tooit. Il file di esempio può essere scaricato dal [repository Git di Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Può essere scaricato dall'[Area download Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Creare un report in Power BI Desktop
1. Avviare Power BI Desktop sul computer.
2. Da hello **Home** della barra multifunzione, fare clic su **recupera dati**, quindi fare clic su informazioni. In hello **recupera dati** la finestra di dialogo, fare clic su **Azure**, fare clic su **archivio Azure Data Lake**, quindi fare clic su **Connetti**.
   
    ![Connetti tooData Lake archivio](./media/data-lake-store-power-bi/get-data-lake-store-account.png "Connetti tooData Lake archivio")
3. Se viene visualizzato una finestra di dialogo informazioni sul connettore hello in fase di sviluppo, scegliere toocontinue.
4. In hello **Microsoft Azure Data Lake Store** nella finestra di dialogo specificare account archivio Data Lake di hello URL tooyour e quindi fare clic su **OK**.
   
    ![URL di Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL di Data Lake Store")
5. In hello successiva finestra di dialogo, fare clic su **Accedi** toosign in account archivio Data Lake. Verrà reindirizzati nella pagina di accesso dell'organizzazione tooyour. Seguire hello richieste toosign conto hello.
   
    ![Accedere a Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Accedere a Data Lake Store")
6. Dopo aver completato l'accesso, fare clic su **Connetti**.
   
    ![Connetti tooData Lake archivio](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "Connetti tooData Lake archivio")
7. Hello successiva finestra di dialogo Mostra file hello caricato account archivio Data Lake tooyour. Verificare le informazioni di hello e quindi fare clic su **carico**.
   
    ![Caricare dati da Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Caricare dati da Data Lake Store")
8. Al termine dati hello caricati in Power BI, si noterà hello seguenti campi hello **campi** scheda.
   
    ![Campi importati](./media/data-lake-store-power-bi/imported-fields.png "Campi importati")
   
    Tuttavia, toovisualize e analizzare i dati di hello, preferiamo hello toobe di dati disponibili per i seguenti campi hello
   
    ![Campi desiderati](./media/data-lake-store-power-bi/desired-fields.png "Campi desiderati")
   
    Nei passaggi successivi hello, Microsoft aggiornerà hello query tooconvert importato dati hello nel formato desiderato hello.
9. Da hello **Home** della barra multifunzione, fare clic su **modifica query**.
   
    ![Modifica query](./media/data-lake-store-power-bi/edit-queries.png "Modifica query")
10. Nell'Editor di Query di hello in hello **contenuto** colonna, fare clic su **binario**.
    
    ![Modifica query](./media/data-lake-store-power-bi/convert-query1.png "Modifica query")
11. Si noterà un'icona di file, che rappresenta hello **Drivers.txt** file caricato. Fare clic sul file hello e fare clic su **CSV**.    
    
    ![Modifica query](./media/data-lake-store-power-bi/convert-query2.png "Modifica query")
12. L'output sarà come quello illustrato di seguito. I dati sono ora disponibili in un formato che è possibile utilizzare visualizzazioni toocreate.
    
    ![Modifica query](./media/data-lake-store-power-bi/convert-query3.png "Modifica query")
13. Da hello **Home** della barra multifunzione, fare clic su **chiudere e applicare**, quindi fare clic su **chiudere e applicare**.
    
    ![Modifica query](./media/data-lake-store-power-bi/load-edited-query.png "Modifica query")
14. Una volta query hello viene aggiornato, hello **campi** scheda verrà visualizzato hello nuovi campi disponibili per la visualizzazione.
    
    ![Campi aggiornati](./media/data-lake-store-power-bi/updated-query-fields.png "Campi aggiornati")
15. Possiamo creare un grafico a torta di toorepresent driver hello in ogni città per un determinato paese. toodo in tal caso, verificare le selezioni seguenti hello.
    
    1. Dalla scheda visualizzazioni hello, fare clic sul simbolo hello per un grafico a torta.
       
        ![Creare un grafico a torta](./media/data-lake-store-power-bi/create-pie-chart.png "Creare un grafico a torta")
    2. le colonne Hello verrà toouse sono **colonna 4** (nome di città hello) e **colonna 7** (nome di paese hello). Trascinare le colonne dalla **campi** scheda troppo**visualizzazioni** scheda come illustrato di seguito.
       
        ![Creare visualizzazioni](./media/data-lake-store-power-bi/create-visualizations.png "Creare visualizzazioni")
    3. grafico a torta Hello dovrebbe essere simile ad esempio hello illustrato di seguito.
       
        ![Grafico a torta](./media/data-lake-store-power-bi/pie-chart.png "Creare visualizzazioni")
16. Se si seleziona un paese specifico da filtri a livello di pagina hello, è ora possibile visualizzare il numero di hello dei driver in ogni città del paese hello selezionato. Ad esempio, in hello **visualizzazioni** scheda **filtri a livello di pagina**selezionare **Brasile**.
    
    ![Selezionare un paese](./media/data-lake-store-power-bi/select-country.png "Selezionare un paese")
17. grafico a torta Hello è toodisplay aggiornate automaticamente i driver di hello in città hello del Brasile.
    
    ![Conducenti in un paese](./media/data-lake-store-power-bi/driver-per-country.png "Conducenti in un paese")
18. Da hello **File** menu, fare clic su **salvare** visualizzazione hello toosave come un file di Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Pubblicare report tooPower BI servizio
Dopo aver creato visualizzazioni hello in Power BI Desktop, è possibile condividere con altri utenti tramite la pubblicazione di servizi di Power BI toohello. Per istruzioni su come toodo che, vedere [pubblicare da Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Vedere anche
* [Analizzare i dati in Archivio Data Lake con Analisi Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

