---
title: Automation DSC per Azure reporting dati tooOMS Analitica Log aaaForward | Documenti Microsoft
description: In questo articolo viene illustrato come toosend Desired Configuration (DSC) dati tooMicrosoft Operations Management Suite Log Analitica toodeliver informazioni dettagliate e gestione di reporting di stato.
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Inoltrare reporting dati tooOMS Analitica Log DSC di automazione di Azure

Automazione può inviare DSC nodo stato dati tooyour Analitica di Log di Microsoft Operations Management Suite (OMS) dell'area di lavoro.  
Lo stato di conformità è visibile nel portale di Azure hello, o con PowerShell, per i nodi e per singole risorse DSC in configurazioni del nodo. Con Log Analytics è possibile:

* Ottenere le informazioni sulla conformità per i nodi gestiti e le singole risorse
* Attivare un messaggio di posta elettronica o un avviso in base allo stato della conformità
* Scrivere query avanzate nei nodi gestiti
* Correlare lo stato della conformità negli account di Automazione
* Visualizzare la cronologia della conformità dei nodi nel tempo

## <a name="prerequisites"></a>Prerequisiti

toostart Automation DSC per l'invio di report tooLog Analitica, è necessario:

* Hello novembre 2016 o versione successiva versione di [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Un account di automazione di Azure. Per altre informazioni, vedere [Introduzione ad Automazione di Azure](automation-offering-get-started.md)
* Un'area di lavoro di Log Analytics con un'offerta di servizio **Automazione e controllo**. Per altre informazioni, vedere [Introduzione a Log Analytics](../log-analytics/log-analytics-get-started.md).
* Almeno un nodo di Automation DSC per Azure. Per altre informazioni, vedere [Caricamento di computer per la gestione con Automation DSC per Azure](automation-dsc-onboarding.md) 

## <a name="set-up-integration-with-log-analytics"></a>Configurare l'integrazione con Log Analytics

toobegin importazione di dati da Automation DSC per Azure in Log Analitica, hello completo alla procedura seguente:

1. Accedi tooyour account Azure in PowerShell. Vedere [Log in with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0) (Accedere con Azure PowerShell)
1. Ottenere hello _ResourceId_ dell'account di automazione eseguendo il comando PowerShell seguente hello: (se si dispone di più di un account di automazione, scegliere hello _ResourceID_ per conto di hello desiderato tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Ottenere hello _ResourceId_ dell'area di lavoro Analitica Log eseguendo il comando PowerShell seguente hello: (se si dispone di più di un'area di lavoro, scegliere hello _ResourceID_ per area di lavoro hello desiderato tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Hello esecuzione comando PowerShell seguente, sostituendo `<AutomationResourceId>` e `<WorkspaceResourceId>` con hello _ResourceId_ valori da ognuno dei passaggi precedenti hello:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Se si desidera importare dati da Automation DSC per Azure in Log Analitica toostop, eseguire il comando PowerShell seguente hello.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Visualizzare i registri DSC hello

Dopo aver configurato l'integrazione con Log Analitica per i dati di DSC di automazione, un **ricerca nei Log** pulsante verrà visualizzato sulla hello **i nodi DSC** pannello dell'account di automazione. Fare clic su hello **ricerca nei Log** pulsante log hello tooview per dati del nodo DSC.

![Pulsante Ricerca log](media/automation-dsc-diagnostics/log-search-button.png)

Hello **ricerca nei Log** pannello viene aperto e viene visualizzato un **DscNodeStatusData** operazione per ogni nodo DSC e un **DscResourceStatusData** operazione per ogni [DSC risorsa](https://msdn.microsoft.com/powershell/dsc/resources) chiamato nel nodo di hello toothat applicato di configurazione.

Hello **DscResourceStatusData** operazione contiene informazioni sull'errore per tutte le risorse DSC che non è riuscita.

Fare clic su ogni operazione nei dati di hello hello elenco toosee per l'operazione.

È possibile visualizzare anche i registri di hello [ricerca nei Log Analitica. Vedere [Trovare dati tramite ricerche nei log](../log-analytics/log-analytics-log-searches.md).
Digitare quanto segue di hello query toofind il DSC log:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

È inoltre possibile limitare la query hello in base al nome di operazione hello. Ad esempio: 'Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Inviare un messaggio di posta elettronica in caso di errore di un controllo della conformità DSC

Uno dei nostri principali richieste dei clienti è per hello possibilità toosend un messaggio di posta elettronica o un testo quando si verificano problemi con una configurazione DSC.   

la regola toocreate un avviso, è innanzitutto necessario creare una ricerca di log per i record di report DSC hello che deve richiamare avviso hello.  Fare clic su hello **avviso** pulsante toocreate e configurare la regola di avviso hello.

1. Dalla pagina di panoramica Analitica Log hello, fare clic su **ricerca nei Log**.
1. Creare una query di ricerca di log per l'avviso digitando hello dopo una ricerca nel campo query hello:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Se è impostato i log da più di un account o sottoscrizione tooyour area di lavoro automazione, è possibile raggruppare gli avvisi per sottoscrizione e l'account di automazione.  
  Nome dell'account di automazione può essere derivato dal campo risorse hello ricerca hello DscNodeStatusData.  
1. hello tooopen **Aggiungi regola di avviso** schermata, fare clic su **avviso** nella parte superiore di hello della pagina hello. Per ulteriori informazioni sull'avviso hello tooconfigure di hello opzioni, vedere [gli avvisi nel registro Analitica](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Trovare le risorse DSC con errori in tutti i nodi

Un vantaggio dell'uso di Log Analytics consiste nella possibilità di cercare controlli con errori nei nodi.
toofind tutte le istanze di risorse DSC che non è riuscita.

1. Dalla pagina di panoramica Analitica Log hello, fare clic su **ricerca nei Log**.
1. Creare una query di ricerca di log per l'avviso digitando hello dopo una ricerca nel campo query hello:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Visualizzare lo stato cronologico dei nodi DSC

Infine, è opportuno toovisualize la cronologia stato del nodo DSC nel tempo.  
È possibile utilizzare questo toosearch query per lo stato di hello le informazioni sullo stato nodo DSC nel tempo.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Verrà visualizzato un grafico di stato del nodo hello nel tempo.

## <a name="log-analytics-records"></a>Record di Log Analytics

La diagnostica di Automazione di Azure crea due categorie di record in Log Analytics.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Proprietà | Descrizione |
| --- | --- |
| TimeGenerated |Data e l'esecuzione quando il controllo di conformità hello. |
| OperationName |DscNodeStatusData |
| ResultType |Indica se il nodo hello è conforme. |
| NodeName_s |nome Hello del nodo gestito hello. |
| NodeComplianceStatus_s |Indica se il nodo hello è conforme. |
| DscReportStatus |Se il controllo di conformità hello è stato eseguito correttamente. |
| ConfigurationMode | Configurazione hello è come nodo toohello applicato. I valori possibili sono __"ApplyOnly"__,__"ApplyandMonitior"__ e __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC Applica configurazione hello e non esegue altre operazioni, a meno che non viene inserita una nuova configurazione il nodo di destinazione toohello o una nuova configurazione quando viene effettuato il pull da un server. Dopo l'applicazione iniziale di una nuova configurazione, DSC non verifica la deviazione da uno stato configurato in precedenza. DSC tenta configurazione hello tooapply fino a quando non ha esito positivo prima __ApplyOnly__ ha effetto. </li><li> __ApplyAndMonitor__: questo è il valore di predefinito hello. Hello Gestione configurazione locale applica tutte le nuove configurazioni. Dopo l'applicazione iniziale di una nuova configurazione, il nodo di destinazione hello non è sincronizzato con lo stato di hello desiderato, DSC segnala la discrepanza hello nei log. DSC tenta configurazione hello tooapply fino a quando non ha esito positivo prima __ApplyAndMonitor__ ha effetto.</li><li>__ApplyAndAutoCorrect__: DSC applica qualsiasi nuova configurazione. Dopo l'applicazione iniziale di una nuova configurazione, se il nodo di destinazione hello non è sincronizzato con lo stato di hello desiderato, DSC segnala la discrepanza hello nei log e quindi riapplica la configurazione corrente di hello.</li></ul> |
| HostName_s | nome Hello del nodo gestito hello. |
| IPAddress | indirizzo IPv4 Hello di hello gestiti nodo. |
| Categoria | DscNodeStatus |
| Risorsa | nome Hello di hello account di automazione di Azure. |
| Tenant_g | GUID che identifica il tenant di hello per hello chiamante. |
| NodeId_g |GUID che identifica un nodo gestito hello. |
| DscReportId_g |GUID che identifica il report hello. |
| LastSeenTime_t |Data e ora ultima visualizzando i report di hello. |
| ReportStartTime_t |Data e ora di inizio report hello. |
| ReportEndTime_t |Data e ora di completamento report hello. |
| NumberOfResources_d |nel nodo di toohello configurazione applicata hello è definito il numero di Hello di risorse DSC. |
| SourceSystem | Modalità di raccolta dei dati hello Analitica di Log. È sempre *Azure* per la diagnostica di Azure. |
| ResourceId |Specifica l'account di automazione di Azure hello. |
| ResultDescription | descrizione di Hello per questa operazione. |
| SubscriptionId | Hello la sottoscrizione di Azure Id (GUID) per l'account di automazione hello. |
| ResourceGroup | Nome del gruppo di risorse hello per hello account di automazione. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID che rappresenta l'Id di correlazione di report di conformità hello hello. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Proprietà | Descrizione |
| --- | --- |
| TimeGenerated |Data e l'esecuzione quando il controllo di conformità hello. |
| OperationName |DscResourceStatusData|
| ResultType |Indica se la risorsa hello è conforme. |
| NodeName_s |nome Hello del nodo gestito hello. |
| Categoria | DscNodeStatus |
| Risorsa | nome Hello di hello account di automazione di Azure. |
| Tenant_g | GUID che identifica il tenant di hello per hello chiamante. |
| NodeId_g |GUID che identifica un nodo gestito hello. |
| DscReportId_g |GUID che identifica il report hello. |
| DscResourceId_s |nome Hello dell'istanza di risorsa hello DSC. |
| DscResourceName_s |nome di Hello della risorsa DSC hello. |
| DscResourceStatus_s |Se hello risorsa DSC è conforme. |
| DscModuleName_s |nome di Hello del modulo di PowerShell hello che contiene una risorsa DSC hello. |
| DscModuleVersion_s |versione di Hello del modulo di PowerShell hello che contiene una risorsa DSC hello. |
| DscConfigurationName_s |nome Hello della configurazione di hello applicato toohello nodo. |
| ErrorCode_s | codice di errore Hello se hello risorsa non è riuscita. |
| ErrorMessage_s |messaggio di errore Hello se hello risorsa non è riuscita. |
| DscResourceDuration_d |tempo di Hello, in secondi, che hello risorsa DSC è stata eseguita. |
| SourceSystem | Modalità di raccolta dei dati hello Analitica di Log. È sempre *Azure* per la diagnostica di Azure. |
| ResourceId |Specifica l'account di automazione di Azure hello. |
| ResultDescription | descrizione di Hello per questa operazione. |
| SubscriptionId | Hello la sottoscrizione di Azure Id (GUID) per l'account di automazione hello. |
| ResourceGroup | Nome del gruppo di risorse hello per hello account di automazione. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |GUID che rappresenta l'Id di correlazione di report di conformità hello hello. |

## <a name="summary"></a>Riepilogo

Inviando i tooLog dati Automation DSC Analitica, è possibile ottenere una migliore comprensione stato hello dei nodi DSC di automazione da:

* Impostazione di avvisi toonotify è quando si verifica un problema
* I risultati di runbook lo stato del processo di runbook e altri con visualizzazioni personalizzate e toovisualize query di ricerca correlato gli indicatori chiave o metrica.  

Log Analitica fornisce maggiore visibilità operational tooyour Automation DSC per dati e consente più rapidamente gli eventi imprevisti di indirizzo.  

## <a name="next-steps"></a>Passaggi successivi

* ulteriori informazioni su come query di ricerca diverso tooconstruct e revisione hello Automation DSC registra con Log Analitica, toolearn vedere [Accedi ricerche Log Analitica](../log-analytics/log-analytics-log-searches.md)
* toolearn ulteriori informazioni sull'utilizzo di Automation DSC per Azure, vedere [Introduzione a DSC di automazione di Azure](automation-dsc-getting-started.md)
* toolearn ulteriori informazioni su OMS Log Analitica e origini di raccolta dati, vedere [dati di archiviazione di Azure la raccolta in panoramica Log Analitica](../log-analytics/log-analytics-azure-storage.md)

