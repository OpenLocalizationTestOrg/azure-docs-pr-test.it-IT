---
title: aaaStarting e arrestare le macchine virtuali - grafico | Documenti Microsoft
description: Versione del flusso di lavoro di PowerShell di scenario di automazione di Azure, inclusi i runbook toostart e arrestare macchine virtuali classiche.
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
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Scenario di Automazione di Azure - Avvio e arresto delle macchine virtuali
Questo scenario di automazione di Azure include runbook toostart e arrestare macchine virtuali classiche.  È possibile utilizzare questo scenario per hello seguenti:  

* Usare i runbook di hello senza alcuna modifica nel proprio ambiente.
* Modificare hello runbook tooperform personalizzato funzionalità.  
* Chiamare hello runbook da un altro runbook come parte di una soluzione completa.
* Usare i runbook di hello come creazione concetti dei runbook toolearn esercitazioni.

> [!div class="op_single_selector"]
> * [Grafico](automation-solution-startstopvm-graphical.md)
> * [Flusso di lavoro PowerShell](automation-solution-startstopvm-psworkflow.md)
>
>

Si tratta hello runbook grafico versione di questo scenario. È disponibile anche usando i [runbook dei flussi di lavoro PowerShell](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Scenario di recupero hello
Questo scenario è costituita da due due runbook grafici che è possibile scaricare da hello seguendo i collegamenti.  Vedere hello [versione del flusso di lavoro di PowerShell](automation-solution-startstopvm-psworkflow.md) di questo scenario per collegamenti toohello runbook del flusso di lavoro di PowerShell.

| Runbook | Collegamento | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Runbook grafico per l'avvio di macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafico |Avvia tutte le macchine virtuali classiche in una sottoscrizione di Azure o tutte le macchine virtuali con un nome di servizio specifico. |
| StopAzureClassicVM |[Runbook grafico per l'arresto di macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafico |Arresta tutte le macchine virtuali in un account di automazione o tutte le macchine virtuali con un nome di servizio specifico. |

## <a name="installing-and-configuring-hello-scenario"></a>Installazione e configurazione di uno scenario di hello
### <a name="1-install-hello-runbooks"></a>1. Installare i runbook hello
Dopo aver scaricato hello runbook, è possibile importarli nella procedura hello in [procedure runbook grafico](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Descrizione di revisione hello e requisiti
i runbook Hello includono un'attività denominata **Leggimi** che include una descrizione e le risorse necessarie.  È possibile visualizzare queste informazioni selezionando hello **Leggimi** attività e quindi hello **Script del flusso di lavoro** parametro.  È inoltre possibile ottenere hello stesse informazioni in questo articolo.

### <a name="3-configure-assets"></a>3. Configurare gli asset
i runbook di Hello richiedono hello seguenti risorse che è necessario creare e popolare con i valori appropriati.  i nomi di Hello sono predefiniti.  È possibile utilizzare gli asset con nomi diversi, se si specificano i nomi in hello [i parametri di input](#using-the-runbooks) quando si avvia runbook hello.

| Tipo di risorsa | Nome predefinito | Descrizione |
|:--- |:--- |:--- |:--- |
| [Credenziali](automation-credentials.md) |AzureCredential |Contiene le credenziali per un account che dispone di autorità toostart e arrestare le macchine virtuali nella sottoscrizione di Azure hello. |
| [Variabile](automation-variables.md) |AzureSubscriptionId |Contiene l'ID sottoscrizione hello della sottoscrizione Azure. |

## <a name="using-hello-scenario"></a>Uno scenario di hello
### <a name="parameters"></a>parameters
ogni runbook Hello sono seguente hello [i parametri di input](automation-starting-a-runbook.md#runbook-parameters).  È necessario fornire valori per tutti i parametri obbligatori ed è possibile facoltativamente specificare i valori per gli altri parametri a seconda delle esigenze.

| Parametro | Tipo | Mandatory | Descrizione |
|:--- |:--- |:--- |:--- |
| ServiceName |string |No |Se viene specificato un valore, verranno avviate o arrestate tutte le macchine virtuali con lo stesso nome di servizio.  Se non viene fornito alcun valore, tutte le macchine virtuali classiche nella sottoscrizione di Azure hello sono avviate o arrestate. |
| AzureSubscriptionIdAssetName |string |No |Contiene il nome di hello di hello [asset della variabile](#installing-and-configuring-the-scenario) che contiene l'ID sottoscrizione hello della sottoscrizione Azure.  Se non si specifica un valore, verrà usato *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |No |Contiene il nome di hello di hello [asset delle credenziali](#installing-and-configuring-the-scenario) che contiene le credenziali di hello per toouse runbook hello.  Se non si specifica un valore, verrà usato *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>Esecuzione dei runbook hello
È possibile utilizzare uno dei metodi di hello in [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md) toostart uno dei runbook hello in questo articolo.

Hello seguenti comandi di esempio utilizza Windows PowerShell toorun **StartAzureClassicVM** toostart tutte le macchine virtuali con il nome di servizio hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Output
i runbook Hello verranno [un messaggio di output](automation-runbook-output-and-messages.md) per ogni macchina virtuale che indica se hello avvio o l'istruzione stop è stata inviata correttamente.  È possibile cercare una stringa specifica in hello output toodetermine hello risultato per ogni runbook.  Nella hello nella tabella seguente sono elencate le stringhe di output possibili Hello.

| Runbook | Condizione | Message |
|:--- |:--- |:--- |
| StartAzureClassicVM |Macchina virtuale già in esecuzione |MyVM is already running |
| StartAzureClassicVM |Richiesta di avvio per la macchina virtuale inviata correttamente |MyVM has been started |
| StartAzureClassicVM |Richiesta di avvio per la macchina virtuale non riuscita |Toostart MyVM non riuscita |
| StopAzureClassicVM |Macchina virtuale già in esecuzione |MyVM is already stopped |
| StopAzureClassicVM |Richiesta di avvio per la macchina virtuale inviata correttamente |MyVM has been started |
| StopAzureClassicVM |Richiesta di avvio per la macchina virtuale non riuscita |Toostart MyVM non riuscita |

Di seguito è un'immagine dell'utilizzo di hello **StartAzureClassicVM** come un [runbook figlio](automation-child-runbooks.md) in un runbook grafico di esempio.  Usa collegamenti condizionali hello in hello nella tabella seguente.

| Collegamento | Criteri |
|:--- |:--- |
| Collegamento di esito positivo |$ActivityOutput['StartAzureClassicVM'] -like "\*has been started" |
| Collegamento di errore |$ActivityOutput['StartAzureClassicVM'] -notlike "\*has been started" |

![Esempio di runbook figlio](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>Scomposizione dettagliata
Di seguito è una suddivisione dettagliata dei runbook hello in questo scenario.  È possibile utilizzare queste informazioni tooeither personalizzare runbook hello o toolearn solo da essi per la creazione di propri scenari di automazione.

### <a name="authentication"></a>Autenticazione
![Autenticazione](media/automation-solution-startstopvm/graphical-authentication.png)

Hello runbook viene avviato con hello tooset attività [credenziali](automation-credentials.md) e sottoscrizione di Azure che verrà utilizzato per il resto di hello del runbook hello.

le prime due attività, Hello **ottenere l'Id sottoscrizione** e **ottenere credenziali di Azure**, recuperare hello [asset](#installing-the-runbook) utilizzati dalle due attività hello.  Tali attività può specificare direttamente le risorse di hello, ma hanno bisogno i nomi delle risorse hello.  Poiché si consente hello utente toospecify tali nomi in hello [i parametri di input](#using-the-runbooks), abbiamo bisogno di queste risorse hello tooretrieve di attività con un nome specificato da un parametro di input.

**Aggiungere-AzureAccount** hello di set di credenziali da utilizzare per il resto di hello di hello runbook.  asset delle credenziali Hello che viene recuperata dal **ottenere credenziali di Azure** deve avere accesso toostart e arrestare le macchine virtuali nella sottoscrizione di Azure hello.  Hello sottoscrizione utilizzato è selezionata per **Select-AzureSubscription** che utilizza l'Id sottoscrizione hello da **ottenere l'Id sottoscrizione**.

### <a name="get-virtual-machines"></a>Ottenere le macchine virtuali
![Ottenere le macchine virtuali](media/automation-solution-startstopvm/graphical-getvms.png)

Hello runbook deve toodetermine le macchine virtuali che utilizzeranno e che vengono già avviati o interrotto (a seconda di runbook hello).   Uno dei due attività recupererà le macchine virtuali hello.  **Ottenere le macchine virtuali nel servizio** verrà eseguito se hello *ServiceName* parametro di input per hello runbook contiene un valore.  **Ottenere tutte le macchine virtuali** verrà eseguito se hello *ServiceName* parametro di input per hello runbook non contiene un valore.  Questa logica viene eseguita da collegamenti condizionali di hello che precede ogni attività.

Entrambe le attività utilizzano hello **Get-AzureVM** cmdlet.  **Ottenere tutte le macchine virtuali** utilizza hello **ListAllVMs** parametro impostato tooreturn tutte le macchine virtuali.  **Ottenere le macchine virtuali nel servizio** utilizza hello **GetVMByServiceAndVMName** parametro impostato e fornisce hello **ServiceName** parametro di input per hello **ServiceName**parametro.  

### <a name="merge-vms"></a>Unire le macchine virtuali
![Unire le macchine virtuali](media/automation-solution-startstopvm/graphical-mergevms.png)

Hello **macchine virtuali di tipo Merge** attività è necessario tooprovide di input troppo**Start-AzureVM** che necessitano di hello nome e il nome del servizio di hello toostart di macchine virtuali.  Questo input può provenire da **Get All VMs** o **Get VMs in Service**, ma **Start-AzureVM** può specificare una sola attività per l'input.   

scenario di Hello è toocreate **macchine virtuali di tipo Merge** che esegue hello **Write-Output** cmdlet.  Hello **InputObject** parametro per cui un cmdlet è un'espressione di PowerShell che combina input hello delle attività hello due precedenti.  Verrà eseguita una sola di queste attività e pertanto è previsto un solo set di output.  **Start-AzureVM** può usare questo output per i parametri di input.

### <a name="startstop-virtual-machines"></a>Avviare/arrestare macchine virtuali
![Avviare le macchine virtuali](media/automation-solution-startstopvm/graphical-startvm.png) ![Arrestare le macchine virtuali](media/automation-solution-startstopvm/graphical-stopvm.png)

A seconda di hello runbook, le attività successive hello tenta toostart o interrompere l'utilizzo di runbook hello **Start-AzureVM** o **Stop-AzureVM**.  Poiché l'attività hello è preceduta da un collegamento alla pipeline, verrà eseguito una volta per ogni oggetto restituito da **macchine virtuali di tipo Merge**.  Hello collegamento è condizionale in modo che l'attività hello verrà eseguito solo se hello *RunningState* di hello macchina virtuale è *arrestato* per **Start-AzureVM** e  *Avvio* per **Stop-AzureVM**. Se questa condizione non viene soddisfatta, quindi **notificare già avviato** o **notificare già arrestato** eseguire toosend un messaggio utilizzando **Write-Output**.

### <a name="send-output"></a>Inviare l'output
![Notifica di avvio delle macchine virtuali](media/automation-solution-startstopvm/graphical-notifystart.png) ![Notifica di arresto delle macchine virtuali](media/automation-solution-startstopvm/graphical-notifystop.png)

passaggio finale Hello runbook hello è output toosend hello se l'inizio o la richiesta di arresto per ogni macchina virtuale è stata inviata correttamente. È un oggetto separato **Write-Output** attività per ogni, e si determina che uno toorun con collegamenti condizionali.  L'attività **Notify VM Started** o **Notify VM Stopped** verrà eseguita se il valore di *OperationStatus* è *Succeeded*.  Se *Statooperazione* è qualsiasi altro valore, quindi **Impossibile notificare tooStart** o **tooStop Impossibile notificare** viene eseguito.

## <a name="next-steps"></a>Passaggi successivi
* [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md)
* [Runbook figlio in Automazione di Azure](automation-child-runbooks.md)
* [Output di runbook e messaggi in automazione di Azure](automation-runbook-output-and-messages.md)
