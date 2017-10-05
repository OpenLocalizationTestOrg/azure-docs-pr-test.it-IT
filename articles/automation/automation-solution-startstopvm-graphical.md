---
title: Avvio e arresto di macchine virtuali - Runbook grafici | Documentazione Microsoft
description: Versione del flusso di lavoro PowerShell per lo scenario di Automazione di Azure che include runbook per l'avvio e l'arresto delle macchine virtuali classiche.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scenario di Automazione di Azure - Avvio e arresto delle macchine virtuali
Questo scenario di Automazione di Azure include runbook per l'avvio e l'arresto di macchine virtuali classiche.  È possibile usare questo scenario per le operazioni seguenti:  

* Usare i runbook senza modifiche nell'ambiente in uso.
* Modificare i runbook per eseguire funzionalità personalizzate.  
* Chiamare i runbook da un altro runbook come parte di una soluzione completa.
* Usare i runbook come esercitazioni per acquisire familiarità con i concetti di creazione dei runbook.

> [!div class="op_single_selector"]
> * [Grafico](automation-solution-startstopvm-graphical.md)
> * [Flusso di lavoro PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Questa è una versione dello scenario con runbook grafici. È disponibile anche usando i [runbook dei flussi di lavoro PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-the-scenario"></a>Come ottenere lo scenario
Questo scenario è costituito da due runbook grafici che è possibile scaricare dai collegamenti seguenti.  Per i collegamenti ai runbook dei flussi di lavoro PowerShell, vedere la [versione dei flussi di lavoro PowerShell](automation-solution-startstopvm-psworkflow.md) di questo scenario.

| Runbook | Collegamento | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Runbook grafico per l'avvio di macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafico |Avvia tutte le macchine virtuali classiche in una sottoscrizione di Azure o tutte le macchine virtuali con un nome di servizio specifico. |
| StopAzureClassicVM |[Runbook grafico per l'arresto di macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafico |Arresta tutte le macchine virtuali in un account di automazione o tutte le macchine virtuali con un nome di servizio specifico. |

## <a name="installing-and-configuring-the-scenario"></a>Installazione e configurazione dello scenario
### <a name="1-install-the-runbooks"></a>1. Installare i runbook
Dopo aver scaricato i runbook, è possibile importarli usando la procedura descritta nell'articolo relativo alle [procedure per i runbook grafici](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-the-description-and-requirements"></a>2. Esaminare la descrizione e i requisiti
I runbook includono un'attività denominata **Read Me** che include una descrizione e gli asset necessari.  Per visualizzare queste informazioni, selezionare l'attività **Read Me** e quindi il parametro **Workflow Script**.  Le stesse informazioni sono disponibili anche in questo articolo.

### <a name="3-configure-assets"></a>3. Configurare gli asset
I runbook richiedono gli asset seguenti, che devono essere creati e popolati con i valori appropriati.  I nomi sono predefiniti.  È possibile usare asset con nomi diversi se tali nomi vengono specificati nei [parametri di input](#using-the-runbooks) all'avvio del runbook.

| Tipo di risorsa | Nome predefinito | Descrizione |
|:--- |:--- |:--- |:--- |
| [Credenziali](automation-credentials.md) |AzureCredential |Contiene le credenziali per un account che dispone delle autorizzazioni per avviare e arrestare le macchine virtuali nella sottoscrizione di Azure. |
| [Variabile](automation-variables.md) |AzureSubscriptionId |Contiene l'ID sottoscrizione della sottoscrizione di Azure. |

## <a name="using-the-scenario"></a>Uso dello scenario
### <a name="parameters"></a>Parametri
Ogni runbook è associato ai [parametri di input](automation-starting-a-runbook.md#runbook-parameters)seguenti.  È necessario fornire valori per tutti i parametri obbligatori ed è possibile facoltativamente specificare i valori per gli altri parametri a seconda delle esigenze.

| Parametro | Tipo | Mandatory | Descrizione |
|:--- |:--- |:--- |:--- |
| ServiceName |string |No |Se viene specificato un valore, verranno avviate o arrestate tutte le macchine virtuali con lo stesso nome di servizio.  Se invece non viene specificato alcun valore, verranno avviate o arrestate tutte le macchine virtuali classiche della sottoscrizione di Azure. |
| AzureSubscriptionIdAssetName |string |No |Contiene il nome dell' [asset di tipo variabile](#installing-and-configuring-the-scenario) che include l'ID sottoscrizione della sottoscrizione di Azure.  Se non si specifica un valore, verrà usato *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |No |Contiene il nome dell' [asset di tipo credenziali](#installing-and-configuring-the-scenario) che include le credenziali per il runbook da usare.  Se non si specifica un valore, verrà usato *AzureCredential* . |

### <a name="starting-the-runbooks"></a>Avvio dei runbook
È possibile usare uno dei metodi descritti in [Avvio di un Runbook in Automazione di Azure](automation-starting-a-runbook.md) per avviare uno dei runbook di questo articolo.

I comandi di esempio seguenti usano Windows PowerShell per eseguire **StartAzureClassicVM** per avviare tutte le macchine virtuali con nome di servizio *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Output
I runbook [restituiranno un messaggio](automation-runbook-output-and-messages.md) per ogni macchina virtuale indicando se l'istruzione di avvio o di arresto è stata inviata correttamente.  È possibile cercare una stringa specifica nell'output per determinare il risultato per ogni runbook.  Nella tabella seguente sono elencate le stringhe di output possibili.

| Runbook | Condizione | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |Macchina virtuale già in esecuzione |MyVM is already running |
| StartAzureClassicVM |Richiesta di avvio per la macchina virtuale inviata correttamente |MyVM has been started |
| StartAzureClassicVM |Richiesta di avvio per la macchina virtuale non riuscita |MyVM failed to start |
| StopAzureClassicVM |Macchina virtuale già in esecuzione |MyVM is already stopped |
| StopAzureClassicVM |Richiesta di avvio per la macchina virtuale inviata correttamente |MyVM has been started |
| StopAzureClassicVM |Richiesta di avvio per la macchina virtuale non riuscita |MyVM failed to start |

Viene riportata di seguito un'immagine dell'uso di **StartAzureClassicVM** come [runbook figlio](automation-child-runbooks.md) in un runbook grafico di esempio.  Vengono usati i collegamenti condizionali indicati nella tabella seguente.

| Collegamento | Criteri |
|:--- |:--- |
| Collegamento di esito positivo |$ActivityOutput['StartAzureClassicVM'] -like "\*has been started" |
| Collegamento di errore |$ActivityOutput['StartAzureClassicVM'] -notlike "\*has been started" |

![Esempio di runbook figlio](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Scomposizione dettagliata
Di seguito è riportata una scomposizione dettagliata dei runbook di questo scenario.  È possibile usare queste informazioni per personalizzare i runbook o semplicemente per acquisire familiarità per la creazione di scenari di automazione personalizzati.

### <a name="authentication"></a>Autenticazione
![Autenticazione](media/automation-solution-startstopvm/graphical-authentication.png)

Le attività iniziali del runbook impostano le [credenziali](automation-credentials.md) e la sottoscrizione di Azure che verranno usate per il resto del runbook.

Le prime due attività, **Get Subscription Id** e **Get Azure Credential**, recuperano gli [asset](#installing-the-runbook) usati dalle due attività successive.  Queste attività possono specificare direttamente gli asset, ma necessitano dei nomi.  Poiché si consente all'utente di specificare i nomi nei [parametri di input](#using-the-runbooks), queste attività sono necessarie per recuperare gli asset con un nome specificato da un parametro di input.

**Add-AzureAccount** imposta le credenziali che verranno usate per il resto del runbook.  L'asset di tipo credenziali che recupera da **Get Azure Credential** deve disporre dell'accesso per l'avvio e l'arresto delle macchine virtuali nella sottoscrizione di Azure.  La sottoscrizione usata viene selezionata da **Select-AzureSubscription**, che usa l'ID sottoscrizione ottenuto da **Get Subscription Id**.

### <a name="get-virtual-machines"></a>Ottenere le macchine virtuali
![Ottenere le macchine virtuali](media/automation-solution-startstopvm/graphical-getvms.png)

Il runbook deve stabilire quali macchine virtuali verranno usate e se sono già avviate o arrestate (a seconda del runbook).   Una delle due attività recupererà le macchine virtuali.  **Get VMs in Service** verrà eseguita se il parametro di input *ServiceName* del runbook contiene un valore.  **Get All VMs** verrà eseguita se il parametro di input *ServiceName* del runbook non contiene alcun valore.  Questa logica viene eseguita dai collegamenti condizionali che precedono ogni attività.

Entrambe le attività usano il cmdlet **Get-AzureVM** .  **Get All VMs** usa il set di parametri **ListAllVMs** per restituire tutte le macchine virtuali.  **Get VMs in Service** usa il set di parametri **GetVMByServiceAndVMName** e fornisce il parametro di input **ServiceName** per il parametro **ServiceName**.  

### <a name="merge-vms"></a>Unire le macchine virtuali
![Unire le macchine virtuali](media/automation-solution-startstopvm/graphical-mergevms.png)

L'attività **Merge VMs** è necessaria per fornire l'input a **Start-AzureVM**, che necessita del nome del servizio e del nome delle VM da avviare.  Questo input può provenire da **Get All VMs** o **Get VMs in Service**, ma **Start-AzureVM** può specificare una sola attività per l'input.   

Lo scenario consiste nel creare un'attività **Merge VMs** che esegue il cmdlet **Write-Output**.  Il parametro **InputObject** per tale cmdlet è un'espressione di PowerShell che combina l'input delle due attività precedenti.  Verrà eseguita una sola di queste attività e pertanto è previsto un solo set di output.  **Start-AzureVM** può usare questo output per i parametri di input.

### <a name="startstop-virtual-machines"></a>Avviare/arrestare macchine virtuali
![Avviare le macchine virtuali](media/automation-solution-startstopvm/graphical-startvm.png) ![Arrestare le macchine virtuali](media/automation-solution-startstopvm/graphical-stopvm.png)

A seconda del runbook, le attività successive provano ad avviare o arrestare il runbook usando **Start-AzureVM** o **Stop-AzureVM**.  Poiché l'attività è preceduta da un collegamento di tipo pipeline, verrà eseguita una volta per ogni oggetto restituito da **Merge VMs**.  Il collegamento è di tipo condizionale, quindi l'attività verrà eseguita soltanto se il valore *RunningState* della macchina virtuale è *Stopped* per **Start-AzureVM** e *Started* per **Stop-AzureVM**. Se questa condizione non viene soddisfatta, verrà eseguita l'attività **Notify Already Started** o **Notify Already Stopped** per inviare un messaggio con **Write-Output**.

### <a name="send-output"></a>Inviare l'output
![Notifica di avvio delle macchine virtuali](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notifica di arresto delle macchine virtuali](media/automation-solution-startstopvm/graphical-notifystop.png)

Il passaggio finale del runbook consiste nell'inviare l'output a seconda che la richiesta di avvio o di arresto di ogni macchina virtuale sia stata inviata correttamente. Esiste un'attività separata **Write-Output** per ogni situazione e per determinare quale eseguire vengono usati collegamenti condizionali.  L'attività **Notify VM Started** o **Notify VM Stopped** verrà eseguita se il valore di *OperationStatus* è *Succeeded*.  Se *OperationStatus* è impostato su un altro valore, verrà eseguita l'attività **Notify Failed To Start** o **Notify Failed to Stop**.

## <a name="next-steps"></a>Passaggi successivi
* [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md)
* [Runbook figlio in Automazione di Azure](automation-child-runbooks.md)
* [Output di runbook e messaggi in automazione di Azure](automation-runbook-output-and-messages.md)
