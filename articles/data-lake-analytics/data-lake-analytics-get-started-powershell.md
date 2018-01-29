---
title: Introduzione ad Azure Data Lake Analytics con Azure PowerShell | Documentazione Microsoft
description: 'Usare Azure PowerShell per creare un account di Data Lake Analytics, definire un processo di Data Lake Analytics con U-SQL e inviare il processo. '
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
ms.openlocfilehash: 832a859e70e382eb2eeb41560d1b880f7b87de53
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Introduzione ad Azure Data Lake Analytics con Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Questo articolo illustra come usare Azure PowerShell per creare account Azure Data Lake Analytics e quindi inviare ed eseguire processi U-SQL. Per altre informazioni su Data Lake Analytics, vedere [Panoramica di Azure Data Lake Analytics](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione sono necessari le informazioni seguenti:

* Un **account di Azure Data Lake Analytics**. Vedere [Introduzione a Data Lake Analytics](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Workstation con Azure PowerShell**. Vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-to-azure"></a>Accedere ad Azure

Questa esercitazione presuppone che si abbia già familiarità con l'uso di Azure PowerShell. In particolare, è necessario sapere come accedere ad Azure. Per istruzioni, vedere [Get started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) (Introduzione ad Azure PowerShell).

Per accedere con un nome di sottoscrizione:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Invece del nome della sottoscrizione, è anche possibile usare un ID sottoscrizione per l'accesso:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

In caso di esito positivo, l'output di questo comando è simile al testo seguente:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a>Preparazione dell'esercitazione

I frammenti di codice di PowerShell in questa esercitazione usano le variabili seguenti per archiviare queste informazioni:

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

Creare una variabile di PowerShell per contenere lo script U-SQL.

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
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

Inviare lo script.

```
$job = Submit-AdlJob -Account $adla -Name "My Job" –Script $script
```

In alternativa, è possibile salvare lo script come file ed eseguire l'invio con il comando seguente:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -Account $adla -Name "My Job" –ScriptPath $filename
```


Ottenere lo stato di un processo specifico. Continuare a usare questo cmdlet fino al completamento del processo.

```
$job = Get-AdlJob -Account $adla -JobId $job.JobId
```

Invece di continuare a chiamare Get-AdlAnalyticsJob fino al termine di un processo, è possibile usare il cmdlet Wait-AdlJob.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Scaricare il file di output.

```
Export-AdlStoreItem -Account $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Vedere anche
* Per visualizzare la stessa esercitazione usando altri strumenti, scegliere i selettori di scheda nella parte superiore della pagina.
* Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).
* Per informazioni sulle attività di gestione, vedere [Gestire Azure Data Lake Analytics tramite il portale di Azure](data-lake-analytics-manage-use-portal.md).
