---
title: i log di sito Web aaaAnalyze usando Azure Data Lake Analitica | Documenti Microsoft
description: 'Informazioni su come sito Web tooanalyze registra utilizzando Data Lake Analitica. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Analizzare i log dei siti Web con Azure Data Lake Analytics
Informazioni su come i log di sito Web di tooanalyze tramite Data Lake Analitica, specialmente su come individuare quali riferimenti eseguito errori quando ha tentato di sito Web di hello toovisit.

## <a name="prerequisites"></a>Prerequisiti
* **Visual Studio 2015 o Visual Studio 2013**.
* **[Data Lake Tools per Visual Studio](http://aka.ms/adltoolsvs)**.

    Una volta Data Lake Tools per Visual Studio è installato, verrà visualizzato un **Data Lake** elemento hello **strumenti** menu in Visual Studio:

    ![Menu U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Conoscenza di base del Data Lake Analitica e hello Data Lake Tools per Visual Studio**. tooget introduzione, vedere:

  * [Sviluppare script U-SQL con Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Account Analisi Data Lake.**  Vedere la sezione relativa alla [creazione di un account di Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
* **Caricamento account Data Lake Analitica toohello di hello esempio dati.** Vedere [file di dati di esempio toocopy](data-lake-analytics-get-started-portal.md).

    un processo di Data Lake Analitica toorun, sarà necessario alcuni dati. Anche se hello Data Lake Tools supporta il caricamento di dati, si utilizzerà hello tooupload portale hello esempio dati toomake questa esercitazione toofollow più semplice.

## <a name="connect-tooazure"></a>Connettersi tooAzure
Prima di poter compilare e testare qualsiasi script U-SQL, è necessario innanzitutto connettersi tooAzure.

**tooconnect tooData Lake Analitica**

1. Aprire Visual Studio.
2. Fare clic su **Data Lake > Opzioni e impostazioni**.
3. Fare clic su **Accedi**, o **Cambia utente** se un utente ha effettuato l'accesso e seguire le istruzioni di hello.
4. Fare clic su **OK** finestra Opzioni e impostazioni di hello tooclose.

**toobrowse agli account Data Lake Analitica**

1. In Visual Studio aprire **Esplora server** premendo i tasti **CTRL + ALT + S**.
2. Da **Esplora server** espandere **Azure** e quindi **Data Lake Analytics**. Verrà visualizzato l'elenco degli account di Analisi Data Lake personali, se disponibili. È possibile creare gli account Data Lake Analitica da studio hello. toocreate un account, vedere [Guida introduttiva di Azure Data Lake Analitica tramite il portale di Azure](data-lake-analytics-get-started-portal.md) o [Guida introduttiva di Azure Data Lake Analitica con Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Sviluppare un'applicazione U-SQL
Un'applicazione U-SQL è principalmente uno script U-SQL. toolearn ulteriori informazioni su U-SQL, vedere [introduzione U-SQL](data-lake-analytics-u-sql-get-started.md).

È possibile aggiungere l'applicazione di toohello aggiunta agli operatori definiti dall'utente.  Per altre informazioni, vedere [Sviluppare operatori U-SQL definiti dall'utente per i processi di Analisi Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate e inviare un processo di Data Lake Analitica**

1. Fare clic su hello **File > Nuovo > progetto**.
2. Selezionare il tipo di progetto U-SQL hello.

    ![nuovo progetto U-SQL di Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Fare clic su **OK**. Visual Studio crea una soluzione con un file Script.usql.
4. Immettere lo script seguente nel file Script.usql hello hello:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    hello toounderstand U-SQL, vedere [Introduzione a Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).    
5. Aggiungere un nuovo progetto di tooyour script U-SQL e immettere hello seguente:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Passare script U-SQL prima toohello indietro e Avanti toohello **Invia** pulsante, specificare l'account Analitica.
7. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Build Script** (Compila script). Verificare i risultati di hello nel riquadro di Output di hello.
8. In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Script.usql** e quindi scegliere **Submit Script** (Invia script).
9. Verificare hello **Account Analitica** è hello uno in cui si desidera toorun hello processo e quindi fare clic su **Invia**. Risultati di invio e il collegamento di processo sono disponibili in hello Data Lake Tools per Visual Studio risultati quando viene completato l'invio di hello.
10. Attendere che il processo di hello viene completato correttamente.  Se ha esito negativo processo hello, molto probabilmente manca il file di origine hello.  Verificare hello nella sezione dei prerequisiti di questa esercitazione. Per altre informazioni sulla risoluzione dei problemi, vedere [Monitoraggio e risoluzione dei problemi dei processi di Analisi Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Al termine dell'esecuzione processo hello, vedrai hello seguente schermata:

    ![Analisi Data Lake analizzare i log dei siti Web log dei siti Web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Ripetere i passaggi da 7 a 10 per **Script1.usql**.

**output del processo hello toosee**

1. Da **Esplora Server**, espandere **Azure**, espandere **Data Lake Analitica**, espandere l'account Data Lake Analitica **gliaccountdiarchiviazione**, fare doppio clic su account di archiviazione dei dati Lake hello predefinito e quindi fare clic su **Esplora**.
2. Fare doppio clic su **esempi** tooopen hello cartella e quindi fare doppio clic su **output**.
3. Fare doppio clic su **UnsuccessfulResponsees.log**.
4. È possibile anche fare doppio clic sul file di output di hello in visualizzazione grafico hello del processo di hello in ordine toonavigate direttamente toohello output.

## <a name="see-also"></a>Vedere anche
tooget introduttiva Data Lake Analitica usando strumenti diversi, vedere:

* [Introduzione a Analisi Data Lake tramite il portale di Azure](data-lake-analytics-get-started-portal.md)
* [Introduzione ad Azure Data Lake Analytics con Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introduzione ad Analisi Data Lake mediante .NET SDK](data-lake-analytics-get-started-net-sdk.md)
