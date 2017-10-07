---
title: aaaStarting e l'arresto di macchine virtuali con automazione di Azure - flusso di lavoro PowerShell | Documenti Microsoft
description: Versione con interfaccia grafica dello scenario di automazione di Azure inclusi runbook toostart e arrestare macchine virtuali classiche.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
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

Si tratta di hello versione del runbook del flusso di lavoro di PowerShell di questo scenario. È disponibile anche usando [runbook grafici](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Scenario di recupero hello
Questo scenario è costituito da due runbook del flusso di lavoro di PowerShell che è possibile scaricare da hello seguenti collegamenti.  Vedere hello [versione grafica](automation-solution-startstopvm-graphical.md) di questo scenario per i runbook grafici toohello di collegamenti.

| Runbook | Collegamento | Tipo | Descrizione |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Avviare le macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Flusso di lavoro PowerShell |Avvia tutte le macchine virtuali classiche in una sottoscrizione di Azure o tutte le macchine virtuali con un nome di servizio specifico. |
| Stop-AzureVMs |[Arrestare le macchine virtuali classiche di Azure](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Flusso di lavoro PowerShell |Arresta tutte le macchine virtuali in un account di automazione o tutte le macchine virtuali con un nome di servizio specifico. |

## <a name="installing-and-configuring-hello-scenario"></a>Installazione e configurazione di uno scenario di hello
### <a name="1-install-hello-runbooks"></a>1. Installare i runbook hello
Dopo aver scaricato hello runbook, è possibile importarli nella procedura hello in [importazione di un Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Descrizione di revisione hello e requisiti
i runbook Hello includono il testo della Guida in linea impostata come commento che include una descrizione e le risorse necessarie.  È inoltre possibile ottenere hello stesse informazioni in questo articolo.

### <a name="3-configure-assets"></a>3. Configurare gli asset
i runbook di Hello richiedono hello seguenti risorse che è necessario creare e popolare con i valori appropriati.

| Tipo di risorsa | Nome dell’asset | Descrizione |
|:--- |:--- |:--- |:--- |
| Credenziali |AzureCredential |Contiene le credenziali per un account che dispone di autorità toostart e arrestare le macchine virtuali nella sottoscrizione di Azure hello.  In alternativa, è possibile specificare un altro asset delle credenziali in hello **credenziali** parametro di hello **Add-AzureAccount** attività. |
| Variabile |AzureSubscriptionId |Contiene l'ID sottoscrizione hello della sottoscrizione Azure. |

## <a name="using-hello-scenario"></a>Uno scenario di hello
### <a name="parameters"></a>parameters
ogni runbook Hello avere hello seguenti parametri.  È necessario fornire valori per tutti i parametri obbligatori ed è possibile facoltativamente specificare i valori per gli altri parametri a seconda delle esigenze.

| Parametro | Tipo | Mandatory | Descrizione |
|:--- |:--- |:--- |:--- |
| ServiceName |string |No |Se viene specificato un valore, verranno avviate o arrestate tutte le macchine virtuali con lo stesso nome di servizio.  Se non viene fornito alcun valore, tutte le macchine virtuali classiche nella sottoscrizione di Azure hello sono avviate o arrestate. |
| AzureSubscriptionIdAssetName |string |No |Contiene il nome di hello di hello [asset della variabile](#installing-and-configuring-the-scenario) che contiene l'ID sottoscrizione hello della sottoscrizione Azure.  Se non si specifica un valore, verrà usato *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |No |Contiene il nome di hello di hello [asset delle credenziali](#installing-and-configuring-the-scenario) che contiene le credenziali di hello per toouse runbook hello.  Se non si specifica un valore, verrà usato *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>Esecuzione dei runbook hello
È possibile utilizzare uno dei metodi di hello in [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md) toostart uno dei runbook hello in questo scenario.

Hello seguenti comandi di esempio utilizza Windows PowerShell toorun **StartAzureVMs** toostart tutte le macchine virtuali con il nome di servizio hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Output
i runbook Hello verranno [un messaggio di output](automation-runbook-output-and-messages.md) per ogni macchina virtuale che indica se hello avvio o l'istruzione stop è stata inviata correttamente.  È possibile cercare una stringa specifica in hello output toodetermine hello risultato per ogni runbook.  Nella hello nella tabella seguente sono elencate le stringhe di output possibili Hello.

| Runbook | Condizione | Message |
|:--- |:--- |:--- |
| Start-AzureVMs |Macchina virtuale già in esecuzione |MyVM is already running |
| Start-AzureVMs |Richiesta di avvio per la macchina virtuale inviata correttamente |MyVM has been started |
| Start-AzureVMs |Richiesta di avvio per la macchina virtuale non riuscita |Toostart MyVM non riuscita |
| Stop-AzureVMs |Macchina virtuale già arrestata |MyVM is already stopped |
| Stop-AzureVMs |Richiesta di arresto per la macchina virtuale inviata correttamente |MyVM è stata già arrestata |
| Stop-AzureVMs |Richiesta di arresto la macchina virtuale non riuscita |Toostop MyVM non riuscita |

Ad esempio, hello seguente frammento di codice da un runbook tenta toostart tutte le macchine virtuali con il nome di servizio hello *MyServiceName*.  Se uno di hello avvia le richieste di errore, è possono eseguire le azioni di errore.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Scomposizione dettagliata
Di seguito è una suddivisione dettagliata dei runbook hello in questo scenario.  È possibile utilizzare queste informazioni tooeither personalizzare runbook hello o toolearn solo da essi per la creazione di propri scenari di automazione.

### <a name="parameters"></a>parameters
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hello flusso di lavoro viene avviata tramite il recupero dei valori hello per hello [i parametri di input](#using-the-scenario).  Se non sono specificati i nomi delle risorse hello vengono usati nomi predefiniti.

### <a name="output"></a>Output
    # Returns strings with status messages
    [OutputType([String])]

Questa riga dichiara che l'output di hello del runbook hello sarà una stringa.  Non è obbligatorio ma è consigliabile per quando il runbook hello viene utilizzato come un [runbook figlio](automation-child-runbooks.md) in modo che un runbook padre conoscano l'output di hello digitare tooexpect.

### <a name="authentication"></a>Autenticazione
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

set di righe successive Hello hello [credenziali](automation-credentials.md) e sottoscrizione di Azure che verrà utilizzato per il resto di hello del runbook hello.
Prima di tutto utilizziamo **Get-AutomationPSCredential** asset hello tooget che contiene le credenziali di hello con accesso toostart e arrestare le macchine virtuali in hello sottoscrizione di Azure. **Aggiungere-AzureAccount** utilizza quindi questo credenziali hello tooset di asset.  output di Hello viene assegnato variabile fittizia tooa in modo che non non è incluso nell'output del runbook hello.  

asset della variabile di Hello con sottoscrizione hello ID viene quindi recuperato con **Get-AutomationVariable** e sottoscrizione hello impostata con **Select-AzureSubscription**.

### <a name="get-vms"></a>Ottenere le macchine virtuali
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** è usato tooretrieve hello hello runbook funzionerà con le macchine virtuali.  Se viene fornito un valore in hello **ServiceName** input variabile, quindi solo hello le macchine virtuali con lo stesso nome di servizio vengono recuperate.  Se invece la variabile **ServiceName** è vuota, verranno recuperate tutte le macchine virtuali.

### <a name="startstop-virtual-machines-and-send-output"></a>Avviare/arrestare le macchine virtuali e inviare l'output
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

le righe successive Hello eseguire ogni macchina virtuale.  Prima di tutto hello **alimentazione** di hello macchina virtuale è toosee selezionata se è già in esecuzione o arrestato, a seconda di hello runbook.  Se è già in stato di destinazione hello, toooutput e si termina di runbook hello viene inviato un messaggio.  In caso contrario, quindi **Start-AzureVM** o **Stop-AzureVM** è utilizzato tooattempt toostart o arrestare hello macchina virtuale con il risultato di hello della variabile di hello richiesta tooa stored.  Un messaggio viene quindi inviato toooutput che specifica se hello richiesta toostart o l'arresto è stata inviata correttamente.

## <a name="next-steps"></a>Passaggi successivi
* toolearn più sull'utilizzo dei runbook figlio, vedere [figlio runbook in automazione di Azure](automation-child-runbooks.md)
* toolearn altre informazioni sull'output di risolvere i messaggi durante l'esecuzione di runbook e toohelp di registrazione, vedere [Runbook output e i messaggi in automazione di Azure](automation-runbook-output-and-messages.md)

