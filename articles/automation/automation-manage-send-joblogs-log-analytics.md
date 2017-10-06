---
title: Automazione di Azure processo dati tooOMS Analitica Log aaaForward | Documenti Microsoft
description: In questo articolo viene illustrato come processo runbook e di stato del processo toosend flussi tooMicrosoft Operations Management Suite Log Analitica toodeliver approfondire le conoscenze e gestione.
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Inoltra lo stato del processo e i flussi di lavoro da automazione tooLog Analitica (OMS)
Automazione può inviare runbook processo lo stato e processo flussi tooyour Analitica di Log di Microsoft Operations Management Suite (OMS) dell'area di lavoro.  Processo di log e flussi di lavoro sono visibili nel portale di Azure hello o con PowerShell, per i singoli processi e ciò consentono tooperform semplice indagini. Con Log Analytics è ora possibile:

* Ottenere informazioni dettagliate sui processi di Automazione.
* Attivare un messaggio e-mail o un avviso in base allo stato del processo del runbook, ad esempio non riuscito o sospeso.
* Scrivere query avanzate nei flussi del processo.
* Correlare i processi tra account di Automazione.
* Visualizzare la cronologia dei processi nel tempo.     

## <a name="prerequisites-and-deployment-considerations"></a>Prerequisiti e considerazioni sulla distribuzione
l'invio dell'automazione toostart registra tooLog Analitica, è necessario:

1. Hello novembre 2016 o versione successiva versione di [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Un'area di lavoro di Log Analytics. Per altre informazioni, vedere [Introduzione a Log Analytics](../log-analytics/log-analytics-get-started.md). 
3. Hello ResourceId per l'account di automazione di Azure

toofind hello ResourceId per l'account di automazione di Azure e i Log Analitica dell'area di lavoro, eseguire hello PowerShell seguente:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Se si hanno più account di automazione o aree di lavoro, nell'output di hello di hello precedenti comandi, trovare hello *nome* tooconfigure necessari e copiare il valore di hello per *ResourceId*.

Se è necessario hello toofind *nome* dell'account di automazione in hello portale di Azure selezionare l'account di automazione da hello **account di automazione** pannello e selezionare **tutte le impostazioni**.  Da hello **tutte le impostazioni** pannello, in **impostazioni Account** selezionare **proprietà**.  In hello **proprietà** pannello, è possibile annotare questi valori.<br> ![Proprietà dell'account di Automazione](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Configurare l'integrazione con Log Analytics
1. Nel computer, avviare **Windows PowerShell** da hello **avviare** dello schermo.  
2. Copiare e incollare hello PowerShell seguenti, quindi modificare il valore di hello hello `$workspaceId` e `$automationAccountId`.  Per hello `-Environment` parametro, i valori validi sono *cloud* o *AzureUSGovernment* a seconda di ambiente cloud hello ci si trova in.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

Dopo aver eseguito questo script, i record in Log Analytics verranno visualizzati entro 10 minuti dalla scrittura di nuovi log o flussi di processo.

log di hello toosee, Esegui hello query della ricerca log Analitica Log seguenti:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Verificare la configurazione
tooconfirm che invia l'account di automazione registri dell'area di lavoro di tooyour Analitica di Log, verificare che la diagnostica siano impostata correttamente sull'account di automazione hello utilizzando hello PowerShell seguente:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

Nell'output di hello verificare quanto segue:
+ In *registri*, hello valore per *abilitato* è *True*
+ valore di Hello *Idareadilavoro* è impostato toohello ResourceId dell'area di lavoro Log Analitica


## <a name="log-analytics-records"></a>Record di Log Analytics
La diagnostica di Automazione di Azure crea due tipi di record in Log Analytics che vengono contrassegnati con il tag **Type=AzureDiagnostics**.

### <a name="job-logs"></a>Log del processo
| Proprietà | Descrizione |
| --- | --- |
| TimeGenerated |Data e ora esecuzione processo del runbook hello. |
| RunbookName_s |nome Hello di hello runbook. |
| Caller_s |Che ha iniziato l'operazione di hello.  I valori possibili sono un indirizzo di posta elettronica o il sistema per i processi pianificati. |
| Tenant_g | GUID che identifica il tenant di hello per hello chiamante. |
| JobId_g |GUID che rappresenta l'Id di processo del runbook hello hello. |
| ResultType |stato di Hello del processo del runbook hello.  I valori possibili sono:<br>- Avviato<br>- Interrotto<br>- Sospeso<br>- Non riuscito<br>- Completato |
| Categoria | Classificazione del tipo di hello dei dati.  Per l'automazione, il valore di hello è JobLogs. |
| OperationName | Specifica il tipo di hello di operazione eseguita in Azure.  Per l'automazione, il valore di hello è processo. |
| Risorsa | Nome dell'account di automazione hello |
| SourceSystem | Modalità di raccolta dei dati hello Analitica di Log. È sempre *Azure* per la diagnostica di Azure. |
| ResultDescription |Descrive lo stato del risultato processo runbook hello.  I valori possibili sono:<br>- Processo avviato<br>- Processo non riuscito<br>- Processo completato |
| CorrelationId |GUID che rappresenta l'Id di correlazione di processo del runbook hello hello. |
| ResourceId |Specifica l'id di risorsa account di automazione di Azure hello di hello runbook. |
| SubscriptionId | Hello la sottoscrizione di Azure Id (GUID) per l'account di automazione hello. |
| ResourceGroup | Nome del gruppo di risorse hello per hello account di automazione. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Flussi del processo
| Proprietà | Descrizione |
| --- | --- |
| TimeGenerated |Data e ora esecuzione processo del runbook hello. |
| RunbookName_s |nome Hello di hello runbook. |
| Caller_s |Che ha iniziato l'operazione di hello.  I valori possibili sono un indirizzo di posta elettronica o il sistema per i processi pianificati. |
| StreamType_s |tipo di Hello del flusso di processo. I valori possibili sono:<br>- Avanzamento<br>- Output<br>- Avviso<br>- Errore<br>- Debug<br>- Dettagliato |
| Tenant_g | GUID che identifica il tenant di hello per hello chiamante. |
| JobId_g |GUID che rappresenta l'Id di processo del runbook hello hello. |
| ResultType |stato di Hello del processo del runbook hello.  I valori possibili sono:<br>- In corso |
| Categoria | Classificazione del tipo di hello dei dati.  Per l'automazione, il valore di hello è JobStreams. |
| OperationName | Specifica il tipo di hello di operazione eseguita in Azure.  Per l'automazione, il valore di hello è processo. |
| Risorsa | Nome dell'account di automazione hello |
| SourceSystem | Modalità di raccolta dei dati hello Analitica di Log. È sempre *Azure* per la diagnostica di Azure. |
| ResultDescription |Include il flusso di output di hello da hello runbook. |
| CorrelationId |GUID che rappresenta l'Id di correlazione di processo del runbook hello hello. |
| ResourceId |Specifica l'id di risorsa account di automazione di Azure hello di hello runbook. |
| SubscriptionId | Hello la sottoscrizione di Azure Id (GUID) per l'account di automazione hello. |
| ResourceGroup | Nome del gruppo di risorse hello per hello account di automazione. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Visualizzazione dei log di Automazione in Log Analytics
Ora che è stato avviato l'invio di tooLog di log del processo automazione Analitica, di seguito viene illustrato cosa si può fare con questi log all'interno di Log Analitica.

log di hello toosee, Esegui hello seguente query:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Inviare un messaggio di posta elettronica quando un processo del runbook non riesce o viene sospeso
Uno dei nostri clienti superiore richiesto è per hello possibilità toosend un messaggio di posta elettronica o un testo quando si verificano problemi con un processo del runbook.   

la regola toocreate un avviso, è innanzitutto necessario creare una ricerca di log per il runbook hello i record dei processi devono richiamare avviso hello.  Fare clic su hello **avviso** pulsante toocreate e configurare la regola di avviso hello.

1. Dalla pagina di panoramica Analitica Log hello, fare clic su **ricerca nei Log**.
2. Creare una query di ricerca di log per l'avviso digitando hello dopo una ricerca nel campo query hello: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` è anche possibile raggruppare da hello RunbookName utilizzando:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Se è impostato i log da più di un account o sottoscrizione tooyour area di lavoro automazione, è possibile raggruppare gli avvisi per sottoscrizione e l'account di automazione.  Nome dell'account di automazione può essere derivato dal campo risorse hello ricerca hello JobLogs.  
3. hello tooopen **Aggiungi regola di avviso** schermata, fare clic su **avviso** nella parte superiore di hello della pagina hello. Per ulteriori dettagli sull'avviso hello tooconfigure di hello opzioni, vedere [gli avvisi nel registro Analitica](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Trovare tutti i processi completati con errori
Inoltre tooalerting sugli errori, è possibile trovare quando un processo del runbook dispone di un errore non irreversibile. In questi casi PowerShell produce un flusso di errore, ma gli errori non irreversibili hello causa toosuspend il processo o non riuscire.    

1. Nell'area di lavoro di Log Analytics fare clic su **Ricerca log**.
2. Nel campo della query hello digitare `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` e quindi fare clic su **ricerca**.

### <a name="view-job-streams-for-a-job"></a>Visualizzare flussi del processo per un processo
Quando si esegue il debug di un processo, è inoltre possibile toolook in flussi di lavoro hello.  Hello query seguente vengono illustrati tutti i flussi di hello per un singolo processo con GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Visualizzare lo stato cronologico del processo
Infine, è opportuno toovisualize la cronologia dei processi nel tempo.  È possibile utilizzare questo toosearch query per lo stato di hello dei processi nel tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Grafico dello stato cronologico del processo OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Riepilogo
Inviando l'automazione processo lo stato e flusso di dati tooLog Analitica, è possibile ottenere una migliore comprensione stato hello dei processi di automazione da:
+ Impostazione di avvisi toonotify è quando si verifica un problema
+ I risultati di runbook lo stato del processo di runbook e altri con visualizzazioni personalizzate e toovisualize query di ricerca correlato gli indicatori chiave o metrica.  

Log Analitica fornisce maggiore visibilità operational tooyour processi di automazione e contribuisce di eventi imprevisti di indirizzi più veloci.  

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni su come query di ricerca diverso tooconstruct e revisione hello automazione del processo di log con Log Analitica, vedere [Accedi ricerche Log Analitica](../log-analytics/log-analytics-log-searches.md)
* toounderstand toocreate e recuperare messaggi di errore e di output dal runbook, vedere [Runbook i messaggi e di output](automation-runbook-output-and-messages.md)
* ulteriori sull'esecuzione di runbook, come i processi del runbook toomonitor e altri dettagli tecnici, vedere toolearn [tenere traccia di un processo del runbook](automation-runbook-execution.md)
* toolearn ulteriori informazioni su OMS Log Analitica e origini di raccolta dati, vedere [dati di archiviazione di Azure la raccolta in panoramica Log Analitica](../log-analytics/log-analytics-azure-storage.md)
