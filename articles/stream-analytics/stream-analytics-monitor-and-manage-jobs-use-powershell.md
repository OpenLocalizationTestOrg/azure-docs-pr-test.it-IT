---
title: aaaMonitor e gestire i processi di flusso Analitica con PowerShell | Documenti Microsoft
description: Informazioni su come toouse toomonitor di cmdlet e PowerShell di Azure e gestire i processi di flusso Analitica.
keywords: Azure PowerShell, cmdlet di Azure PowerShell, comando di PowerShell, script di PowerShell
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a>Monitorare e gestire i processi di Analisi di flusso con i cmdlet di Azure PowerShell
Informazioni su come toomonitor e gestire le risorse di flusso Analitica con i cmdlet di Azure PowerShell e script di powershell che eseguono attività Analitica di flusso di base.

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a>Prerequisiti per l'esecuzione dei cmdlet di Azure PowerShell per Analisi dei flussi
* Creare un gruppo di risorse di Azure nella sottoscrizione. Hello seguito è riportato un esempio di script di PowerShell di Azure. Per informazioni su Azure PowerShell , vedere [Installare e configurare Azure PowerShell](/powershell/azure/overview);  

Azure PowerShell 0.9.8:  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

Azure PowerShell 1.0:  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> Nei processi di Analisi di flusso creati a livello di codice il monitoraggio non è abilitato per impostazione predefinita.  È possibile abilitare manualmente il monitoraggio nel portale di Azure passando la pagina di monitoraggio del processo toohello hello e fare clic sul pulsante Abilita hello o è possibile farlo a livello di codice attenendosi alla seguente procedura hello [Analitica di flusso di Azure - Monitoraggio flusso Analitica processi a livello di programmazione](stream-analytics-monitor-jobs.md).
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a>Cmdlet di Azure PowerShell per Analisi dei flussi
Hello seguendo i cmdlet PowerShell di Azure possa essere utilizzati toomonitor e gestire i processi di Analitica di flusso di Azure. Si noti che sono disponibili diverse versioni di Azure PowerShell. 
**Negli esempi di hello è primo comando hello elencati per Azure PowerShell 0.9.8, hello secondo comando è per Azure PowerShell 1.0.** i comandi di Azure PowerShell 1.0 Hello avrà sempre "Azure Resource Manager" nel comando hello.

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a>Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob
Elenca tutti i processi di flusso Analitica definiti nella sottoscrizione di Azure hello o gruppo di risorse specificato oppure ottiene informazioni sul processo su un processo specifico all'interno di un gruppo di risorse.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob

Questo comando di PowerShell restituisce informazioni su tutti i processi di flusso Analitica hello hello sottoscrizione di Azure.

**Esempio 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

Questo comando di PowerShell restituisce informazioni su tutti i processi di flusso Analitica hello nel gruppo di risorse hello analisi dei flussi-predefinito-centrale-US.

**Esempio 3**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

Questo comando di PowerShell restituisce informazioni sul processo di flusso Analitica hello StreamingJob nel gruppo di risorse hello analisi dei flussi-predefinito-centrale-US.

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a>Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput
Elenca tutti gli input hello definiti in un processo di flusso Analitica specificato oppure ottiene informazioni su un input specifico.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Questo comando di PowerShell restituisce informazioni su tutti gli input hello definito nel processo di hello StreamingJob.

**Esempio 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

Questo comando di PowerShell restituisce informazioni sull'input hello denominato definito nel processo di hello StreamingJob EntryStream.

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a>Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput
Elenca tutti gli output di hello definiti in un processo di flusso Analitica specificato oppure ottiene informazioni su un output specifico.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

Questo comando di PowerShell restituisce informazioni sull'output di hello definito nel processo di hello StreamingJob.

**Esempio 2**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

Questo comando di PowerShell restituisce informazioni sull'output di hello denominato definito nel processo di hello StreamingJob di Output.

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a>Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota
Ottiene informazioni sulla quota di hello di streaming unità in una regione specificata.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

Questo comando di PowerShell restituisce informazioni sulla quota di hello e utilizzo di unità di streaming nell'area Stati Uniti centro hello.

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a>Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation
Ottiene informazioni su una specifica trasformazione definita nel processo di Analisi dei flussi.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Azure PowerShell 1.0:  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

Questo comando di PowerShell restituisce informazioni sulla trasformazione hello chiamato StreamingJob nel processo di hello StreamingJob.

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a>New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput
Crea un nuovo input all'interno di un processo di Analisi dei flussi o aggiorna un input esistente specificato.

Hello nome dell'input hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello. Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.

Se si specifica un input che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello input esistente.

Se si specificano hello – parametro Force e nome di input esistente, verrà sostituita hello input senza conferma.

Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Input (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-input] sezione di hello [flusso Analitica API REST di gestione Libreria riferimenti a][stream.analytics.rest.api.reference].

**Esempio 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

Questo comando di PowerShell crea un nuovo input dal file hello Input.json. Se un input esistente con nome hello specificato nel file di definizione input hello è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.

**Esempio 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

Questo comando di PowerShell crea un nuovo input nel processo di hello chiamato EntryStream. Se un input esistente con questo nome è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.

**Esempio 3**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

Questo comando di PowerShell sostituisce definizione hello hello esistente origine di input denominato EntryStream con definizione hello dal file hello.

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a>New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob
Crea un nuovo processo di flusso Analitica in Microsoft Azure o aggiorna la definizione di hello di un processo esistente specificato.

nome di Hello del processo di hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello. Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.

Se si specifica un nome di processo che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello processo esistente.

Se si specifica hello – parametro Force e specificare un nome di processo esistente, definizione del processo hello verrà sostituito senza conferma.

Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Crea processo di flusso Analitica] [ msdn-rest-api-create-stream-analytics-job] sezione di hello [riferimento all'API REST di flusso Analitica gestione Libreria][stream.analytics.rest.api.reference].

**Esempio 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

Questo comando di PowerShell crea un nuovo processo dalla definizione di hello in JobDefinition.json. Se un processo esistente con nome hello specificato nel file di definizione del processo hello è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.

**Esempio 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

Questo comando di PowerShell sostituisce la definizione di processo hello per StreamingJob.

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a>New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput
Crea un nuovo output all'interno di un processo di Analisi dei flussi o aggiorna un output esistente.  

nome di Hello dell'output di hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello. Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.

Se si specifica un output che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello output esistente.

Se si specificano hello – parametro Force e nome di output esistente, l'output di hello verrà sostituita senza conferma.

Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Output (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-output] sezione di hello [flusso Analitica API REST di gestione Libreria riferimenti a][stream.analytics.rest.api.reference].

**Esempio 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

Questo comando di PowerShell crea un nuovo output chiamato "output" nel processo di hello StreamingJob. Se un output esistente con questo nome è già definito, verrà chiesto di cmdlet hello o meno tooreplace è.

**Esempio 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

Questo comando di PowerShell sostituisce definizione hello per "output" nel processo di hello StreamingJob.

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a>New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation
Crea una nuova trasformazione in un processo di flusso Analitica o aggiorna una trasformazione esistente hello.

nome di Hello della trasformazione hello può essere specificato nel file con estensione JSON hello o sulla riga di comando hello. Se vengono specificati entrambi, il nome di hello nella riga di comando hello deve hello come hello file hello.

Se si specifica una trasformazione che esiste già e non si specifica hello: il parametro Force, hello cmdlet chiederà se tooreplace hello trasformazione esistente.

Se si specifica hello – parametro Force e specificare un nome di trasformazione esistente verrà sostituito trasformazione hello senza conferma.

Per informazioni dettagliate sulla struttura dei file JSON hello e il contenuto, vedere toohello [Create Transformation (Analitica del flusso di Azure)] [ msdn-rest-api-create-stream-analytics-transformation] sezione di hello [gestione Analitica di flusso Raccolta di informazioni di riferimento API REST][stream.analytics.rest.api.reference].

**Esempio 1**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

Questo comando di PowerShell crea una nuova trasformazione chiamata StreamingJobTransform nel processo di hello StreamingJob. Se una trasformazione esistente è già stata definita con lo stesso nome, verrà chiesto di cmdlet hello o meno tooreplace è.

**Esempio 2**

Azure PowerShell 0.9.8:  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

Azure PowerShell 1.0:  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 Questo comando di PowerShell sostituisce la definizione di hello di StreamingJobTransform nel processo di hello StreamingJob.

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a>Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput
Elimina in modo asincrono uno specifico input da un processo di Analisi dei flussi in Microsoft Azure.  
Se si specifica hello – parametro Force, hello di input verrà eliminato senza conferma.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

Questo comando di PowerShell rimuove hello EventStream input nel processo di hello StreamingJob.  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a>Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob
Elimina in modo asincrono uno specifico processo di Analisi dei flussi in Microsoft Azure.  
Se si specifica hello: il parametro Force, hello processo sarà eliminato senza conferma.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Questo comando di PowerShell rimuove il processo di hello StreamingJob.  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a>Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput
Elimina in modo asincrono uno specifico output da un processo di Analisi dei flussi in Microsoft Azure.  
Se si specifica hello: il parametro Force, hello output sarà eliminato senza conferma.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Questo comando di PowerShell rimuove hello output Output nel processo di hello StreamingJob.  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a>Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob
In modo asincrono e avvia un processo di Analisi dei flussi in Microsoft Azure.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Azure PowerShell 1.0:  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

Questo comando di PowerShell avvia hello processo StreamingJob con un'ora di inizio di output personalizzato impostato tooDecember 12, 2012, 12:12:12 UTC.

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a>Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob
Interrompe in modo asincrono l'esecuzione di un processo di Analisi dei flussi in Microsoft Azure e dealloca le risorse in uso. Hello metadati e definizione del processo saranno comunque disponibili nella sottoscrizione tramite il portale di Azure hello e API di gestione, in modo che hello processo può essere modificato e riavviato. È non verrà addebitato un processo in stato arrestato hello.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Azure PowerShell 1.0:  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

Questo comando di PowerShell Arresta il processo di hello StreamingJob.  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a>Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput
Possibilità di hello test del flusso Analitica tooconnect tooa specificato di input.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

Questo stato di connessione PowerShell comando test hello di hello EntryStream in StreamingJob di input.  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a>Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput
Possibilità di hello test del flusso Analitica tooconnect tooa specificato output.

**Esempio 1**

Azure PowerShell 0.9.8:  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Azure PowerShell 1.0:  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

Questo stato di connessione PowerShell comando test hello di hello output Output in StreamingJob.  

## <a name="get-support"></a>Supporto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics). 

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

