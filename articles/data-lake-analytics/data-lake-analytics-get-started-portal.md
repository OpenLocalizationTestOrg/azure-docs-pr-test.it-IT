---
title: aaaGet avviato con Azure Data Lake Analitica tramite il portale di Azure | Documenti Microsoft
description: 'Informazioni su come creare un processo di Data Lake Analitica con U-SQL, hello toouse toocreate portale Azure un account Data Lake Analitica e inviare il processo di hello. '
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Introduzione ad Azure Data Lake Analytics con il portale di Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Informazioni su come toouse hello Azure toocreate portale account di Azure Data Lake Analitica, definire i processi in [U-SQL](data-lake-analytics-u-sql-get-started.md)e l'invio del servizio Data Lake Analitica toohello di processi. Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessaria una **sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Creare un account di Analisi Data Lake

A questo punto, si creerà un Analitica Lake dati e un archivio Data Lake account in hello stesso tempo.  Questo passaggio è semplice e richiede solo circa 60 secondi toofinish.

1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo** >  **Dati e analisi** > **Data Lake Analytics**.
3. Selezionare i valori per hello seguenti elementi:
   * **Nome**: il nome dell'account di Data Lake Analytics deve contenere solo lettere minuscole e numeri.
   * **Sottoscrizione**: scegliere una sottoscrizione di Azure usata per hello account Analitica hello.
   * **Gruppo di risorse**. Selezionare un gruppo di risorse di Azure esistente o crearne uno nuovo.
   * **Località**. Selezionare un data center di Azure per l'account Data Lake Analitica hello.
   * **Archivio Data Lake**: seguire hello istruzione toocreate un nuovo account archivio Data Lake o selezionarne uno esistente. 
4. Selezionare eventualmente un piano tariffario per l'account di Data Lake Analytics.
5. Fare clic su **Crea**. 


## <a name="your-first-u-sql-script"></a>Il primo script U-SQL

Dopo il testo Hello è un semplice script U-SQL. Non è di definire un piccolo set di dati all'interno dello script hello e quindi scrivere set di dati all'archivio Data Lake di toohello predefinito come un file denominato `/data.csv`.

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a>Inviare un processo U-SQL

1. Hello account Data Lake Analitica, fare clic su **nuovo processo**.
2. Incolla il testo hello di hello script U-SQL illustrato in precedenza. 
3. Fare clic su **Submit Job**.   
4. Attendere finché le modifiche di stato processo hello troppo**Succeeded**.
5. Se il processo di hello non riuscito, vedere [monitoraggio e risoluzione dei problemi dei processi di Data Lake Analitica](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Fare clic su hello **Output** scheda e quindi fare clic su `data.csv`. 

## <a name="see-also"></a>Vedere anche

* tooget iniziare a sviluppare applicazioni U-SQL, vedere [script U-SQL sviluppare utilizzando Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).
* Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).
