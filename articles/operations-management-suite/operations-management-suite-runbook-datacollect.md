---
title: aaaCollecting dati Analitica Log con un runbook in automazione di Azure | Documenti Microsoft
description: Esercitazione dettagliata che descrive come creare un runbook nei dati di automazione di Azure toocollect nel repository OMS hello per l'analisi da Analitica di Log.
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Raccogliere dati in Log Analytics con un runbook di Automazione di Azure
È possibile raccogliere una quantità significativa di dati in Log Analytics da una serie di origini, tra cui [origini dati](../log-analytics/log-analytics-data-sources.md) negli agenti e [dati raccolti da Azure](../log-analytics/log-analytics-azure-storage.md).  Esistono un scenari, sebbene in cui è necessario toocollect dati che non sia accessibile tramite queste origini standard.  In questi casi, è possibile utilizzare hello [API dell'agente di raccolta dati di HTTP](../log-analytics/log-analytics-data-collector-api.md) toowrite dati tooLog Analitica da qualsiasi client dell'API REST.  Un esempio di metodo comuni tooperform questa raccolta dati utilizza un runbook in automazione di Azure.   

Questa esercitazione viene descritto il processo di hello per la creazione e pianificazione di un runbook in automazione di Azure toowrite dati tooLog Analitica.


## <a name="prerequisites"></a>Prerequisiti
Questo scenario richiede hello seguenti risorse configurate nella sottoscrizione di Azure.  Per entrambe è possibile usare un account gratuito.

- [Area di lavoro di Log Analytics](../log-analytics/log-analytics-get-started.md).
- [Account di automazione di Azure](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Panoramica dello scenario
Per questa esercitazione si scriverà un runbook che raccoglie informazioni sui processi di automazione.  I runbook in automazione di Azure sono implementati con PowerShell, pertanto si inizierà da scrittura e il test di uno script nell'editor di automazione di Azure hello.  Dopo aver verificato che si raccolgono informazioni hello necessarie, verranno scrivere tale tooLog dati Analitica e verificare il tipo di dati personalizzato hello.  Infine, si creerà un runbook di hello toostart pianificazione a intervalli regolari.

> [!NOTE]
> È possibile configurare l'automazione di Azure toosend processo informazioni tooLog Analitica senza questo runbook.  Questo scenario è principalmente esercitazione di hello toosupport utilizzati e si consiglia di inviare hello tooa test area di lavoro.  


## <a name="1-install-data-collector-api-module"></a>1. Installare il modulo dell'API di raccolta dati
Ogni [richiesta dall'API dell'agente di raccolta dati di HTTP hello](../log-analytics/log-analytics-data-collector-api.md#create-a-request) deve essere formattato in modo appropriato e includere un'intestazione di autorizzazione.  È possibile farlo nel runbook, ma è possibile ridurre la quantità hello del codice necessaria tramite un modulo che semplifica questo processo.  È un modulo che è possibile utilizzare [OMSIngestionAPI modulo](https://www.powershellgallery.com/packages/OMSIngestionAPI) in PowerShell Gallery hello.

toouse un [modulo](../automation/automation-integration-modules.md) in un runbook, deve essere installato nell'account di automazione.  Qualsiasi runbook in hello stesso account può quindi utilizzare hello funzioni nel modulo hello.  È possibile installare un nuovo modulo selezionando **Asset** > **Moduli** > **Aggiungi un modulo** nell'account di Automazione.  

Hello PowerShell Gallery tuttavia offre un toodeploy rapide un modulo direttamente l'account di automazione tooyour pertanto è possibile utilizzare questa opzione per questa esercitazione.  

![Modulo OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Andare troppo[PowerShell Gallery](https://www.powershellgallery.com/).
2. Cercare **OMSIngestionAPI**.
3. Fare clic su hello **distribuire tooAzure automazione** pulsante.
4. Selezionare l'account di automazione e fare clic su **OK** modulo hello tooinstall.


## <a name="2-create-automation-variables"></a>2. Creare variabili di Automazione
Le [variabili di Automazione](..\automation\automation-variables.md) contengono valori che possono essere usati da tutti i runbook presenti nell'account di Automazione.  Rendono i runbook più flessibile, consentendo toochange questi valori senza dover modificare hello runbook effettivo. Ogni richiesta da hello API dell'agente di raccolta dati di HTTP richiede hello ID e la chiave dell'area di lavoro OMS hello e gli asset variabili sono toostore ideale queste informazioni.  

![variables](media/operations-management-suite-runbook-datacollect/variables.png)

1. Nel portale di Azure hello, passare tooyour account di automazione.
2. Selezionare **Variabili** in **Risorse condivise**.
2. Fare clic su **aggiungere una variabile** e creare due variabili hello hello nella tabella seguente.

| Proprietà | Valore ID area di lavoro | Valore chiave area di lavoro |
|:--|:--|:--|
| Nome | WorkspaceId | WorkspaceKey |
| Tipo | String | String |
| Valore | Incollare in hello ID area di lavoro dell'area di lavoro Log Analitica. | Incollare con hello primario o secondario chiave dell'area di lavoro Log Analitica. |
| Crittografato | No | Sì |



## <a name="3-create-runbook"></a>3. Creare un runbook

Automazione di Azure offre un editor nel portale di hello in cui è possibile modificare e testare il runbook.  Si dispone di hello opzione toouse hello script editor toowork con [PowerShell direttamente](../automation/automation-edit-textual-runbook.md) o [creare un runbook grafico](../automation/automation-graphical-authoring-intro.md).  Per questa esercitazione si userà uno script di PowerShell. 

![Modificare il runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Passare tooyour account di automazione.  
2. Fare clic su **Runbook** > **Aggiungi runbook** > **Crea un nuovo runbook**.
3. Per il nome del runbook hello, digitare **raccolta processi di automazione**.  Tipo di runbook hello selezionare **PowerShell**.
4. Fare clic su **crea** toocreate hello runbook e avviare hello dell'editor.
5. Copiare e incollare hello seguente codice all'interno di hello runbook.  Per una spiegazione del codice hello, vedere toohello commenti nello script hello.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Testare il runbook
Automazione di Azure include un ambiente troppo[testare il runbook](../automation/automation-testing-runbook.md) prima della pubblicazione.  È possibile controllare i dati di hello raccolti dal runbook hello e verificare che la scrittura tooLog Analitica come previsto prima di pubblicarlo tooproduction. 
 
![Testare il runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Fare clic su **salvare** toosave hello runbook.
1. Fare clic su **riquadro Test** tooopen hello runbook nell'ambiente di test hello.
3. Poiché il runbook include parametri, è richiesta tooenter valori.  Immettere il nome di hello hello del gruppo di risorse e automazione hello conto che le informazioni di processo corso toocollect da.
4. Fare clic su **avviare** toohello avviare runbook hello.
3. Hello runbook verrà avviato con uno stato di **in coda** prima che diventi troppo**esecuzione**.  
3. Hello runbook deve essere visualizzato un output dettagliato con i processi di hello raccolti in formato json.  Se non è elencato alcun processo, quindi non si è verificato alcun processi creati nell'account di automazione hello in hello ultima ora.  Provare ad avviare qualsiasi runbook nell'account di automazione hello e quindi eseguire di nuovo il test di hello.
4. Verificare che output di hello non mostra che tutti gli errori nella hello post tooLog comando Analitica.  È necessario disporre di seguito toohello simile messaggio.

    ![Output del comando POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Verificare i record in Log Analytics
Una volta hello runbook è stata completata nel test e si è verificato che output di hello è stata ricevuta correttamente, è possibile verificare che i record di hello siano stati creati utilizzando un [ricerca dei registri di Log Analitica](../log-analytics/log-analytics-log-searches.md).

![Output del log](media/operations-management-suite-runbook-datacollect/log-output.png)

1. Nel portale di Azure hello, selezionare l'area di lavoro Log Analitica.
2. Fare clic su **Ricerca log**.
3. Hello tipo comando seguente `Type=AutomationJob_CL` e fare clic sul pulsante ricerca hello. Si noti che tipo di record hello include _CL che non è specificato nello script hello.  Tale suffisso viene automaticamente aggiunto toohello log tipo tooindicate che è un tipo di log personalizzato.
4. Verrà visualizzato uno o più record restituito che indica che runbook hello funzioni come previsto.


## <a name="6-publish-hello-runbook"></a>6. Pubblicare il runbook hello
Dopo aver verificato che runbook hello funzioni correttamente, è necessario toopublish, in modo da eseguire nell'ambiente di produzione.  È possibile continuare tooedit e testare il runbook hello senza modificare la versione pubblicata di hello.  

![Pubblicare il runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Restituire tooyour account di automazione.
2. Fare clic su **Runbook** e selezionare **Collect-Automation-jobs**.
3. Fare clic su **Modifica** e quindi su **Pubblica**.
4. Fare clic su **Sì** quando tooverify frequenti che si desidera toooverwrite hello precedentemente pubblicata versione.

## <a name="7-set-logging-options"></a>7. Impostare le opzioni di registrazione 
Per test, è stato in grado di tooview [output dettagliato](../automation/automation-runbook-output-and-messages.md#message-streams) perché è impostata la variabile hello $VerbosePreference nello script hello.  Per la produzione, le proprietà di registrazione di hello tooset per runbook hello è necessario se si desidera tooview un output dettagliato.  Per i runbook hello utilizzati in questa esercitazione, verrà visualizzato i dati json hello inviati tooLog Analitica.

![Registrazione e traccia](media/operations-management-suite-runbook-datacollect/logging.png)

1. Selezionare la proprietà hello per il runbook **registrazione e traccia** in **delle impostazioni dei Runbook**.
2. Modifica dell'impostazione di hello per **registrazione dei record dettagliati** troppo**su**.
3. Fare clic su **Salva**.

## <a name="8-schedule-runbook"></a>8. Pianificare il runbook
più comuni toostart modo un runbook che raccoglie i dati di monitoraggio Hello è tooschedule è toorun automaticamente.  Questo scopo è la creazione di un [pianificazione in automazione di Azure](../automation/automation-schedules.md) e collegarlo tooyour runbook.

![Pianificare il runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. Nelle proprietà hello runbook, selezionare **pianificazioni** in **risorse**.
2. Fare clic su **aggiungere una pianificazione** > **collega un runbook tooyour pianificazione** > **creare una nuova pianificazione**.
5. Tipo di hello seguenti valori per la pianificazione hello e fare clic su **crea**.

| Proprietà | Valore |
|:--|:--|
| Nome | AutomationJobs-Hourly |
| Inizia | Selezionare qualsiasi tempo di almeno 5 minuti precedenti hello ora corrente. |
| Ricorrenza | Ricorrente |
| Ricorre ogni | 1 ora |
| Imposta scadenza | No |

Dopo aver creata la pianificazione hello, è necessario tooset hello i valori dei parametri da utilizzare ogni volta che la pianificazione avvia runbook hello.

6. Fare clic su **Configura i parametri e le impostazioni di esecuzione**.
7. Specificare i valori per **ResourceGroupName** e **AutomationAccountName**.
8. Fare clic su **OK**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Verificare che il runbook venga avviato secondo la pianificazione
Ogni volta che un runbook viene avviato, [viene creato un processo](../automation/automation-runbook-execution.md) e l'output viene registrato.  In realtà, questi sono hello stessi processi che hello runbook è la raccolta.  È possibile verificare i che runbook hello viene avviato come previsto selezionando i processi di hello per hello runbook dopo che è trascorso l'ora di inizio hello pianificazione hello.

![Processi](media/operations-management-suite-runbook-datacollect/jobs.png)

1. Nelle proprietà hello runbook, selezionare **processi** in **risorse**.
2. Verrà visualizzato che un elenco di processi per ogni runbook hello ora è stato avviato.
3. Fare clic su uno dei hello processi tooview i dettagli.
4. Fare clic su **tutti i log** tooview hello output di hello runbook e registri.
5. Scorrere nella parte inferiore di toohello toofind voce simile toohello immagine riportata di seguito.<br>![Dettagliato](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Fare clic su questa voce tooview hello in dettaglio i dati json che è stati inviati tooLog Analitica.



## <a name="next-steps"></a>Passaggi successivi
- Utilizzare [Visualizza finestra di progettazione](../log-analytics/log-analytics-view-designer.md) toocreate per la visualizzazione di una visualizzazione dati che raccolti repository Analitica Log toohello di hello.
- Creare un pacchetto il runbook in un [soluzione di gestione](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Altre informazioni su [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).
- Altre informazioni su [Automazione di Azure](https://docs.microsoft.com/azure/automation/).
- Altre informazioni su hello [API dell'agente di raccolta dati di HTTP](../log-analytics/log-analytics-data-collector-api.md).
