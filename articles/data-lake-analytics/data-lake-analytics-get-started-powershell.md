---
title: aaaGet avviato con Azure Data Lake Analitica con Azure PowerShell | Documenti Microsoft
description: 'Usare Azure PowerShell toocreate un account Data Lake Analitica, creare un processo di Data Lake Analitica utilizzando U-SQL e inviare il processo di hello. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Introduzione ad Azure Data Lake Analytics con Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Informazioni su come toouse toocreate Azure PowerShell Azure Data Lake Analitica account e quindi inviare ed eseguire i processi di U-SQL. Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, è necessario disporre di hello le seguenti informazioni:

* Un **account di Azure Data Lake Analytics**. Vedere [Introduzione a Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Workstation con Azure PowerShell**. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Accedi tooAzure

Questa esercitazione presuppone che si abbia già familiarità con l'uso di Azure PowerShell. In particolare, è necessario come tooknow toolog in tooAzure. Vedere hello [Guida introduttiva di Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) per assistenza.

toolog con un nome di sottoscrizione:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Anziché il nome di sottoscrizione hello, è inoltre possibile utilizzare un toolog id sottoscrizione in:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

Se ha esito positivo, l'output di hello di questo comando sarà analogo hello seguente testo:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Preparazione per l'esercitazione hello

frammenti di codice PowerShell Hello in questa esercitazione usare questi toostore variabili queste informazioni:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Ottenere informazioni su un account Data Lake Analytics account

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Inviare un processo U-SQL

Creare uno script di PowerShell toohold variabile hello U-SQL.

```
$script = @"
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

"@
```

Inviare script hello.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

In alternativa, è possibile salvare script hello come un file e inviare hello comando seguente:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Ottenere lo stato di hello di un processo specifico. Continuare a utilizzare questo cmdlet fino a visualizzare hello processo viene eseguito.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Anziché chiamare Get AdlAnalyticsJob ripetutamente finché non termina un processo, è possibile utilizzare i cmdlet di attesa AdlJob hello.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Scaricare il file di output di hello.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Vedere anche
* toosee hello stesso esercitazione con altri strumenti, fare clic sui selettori di hello scheda nella parte superiore di hello della pagina hello.
* toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).
* Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).
