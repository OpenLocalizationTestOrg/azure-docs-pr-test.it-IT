---
title: un runbook di automazione di Azure con un webhook aaaStarting | Documenti Microsoft
description: Un webhook che consente a un client toostart un runbook in automazione di Azure da una chiamata HTTP.  Questo articolo viene descritto come toocreate un webhook e come toocall uno toostart un runbook.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Avviare un runbook di Automazione di Azure con un webhook
Oggetto *webhook* consente toostart un determinato runbook in automazione di Azure tramite una singola richiesta HTTP. In questo modo i servizi esterni, ad esempio Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analitica o applicazioni personalizzate toostart runbook senza implementare una soluzione completa utilizzando hello API di automazione di Azure.  
![Panoramica dei webhook](media/automation-webhooks/webhook-overview-image.png)

È possibile confrontare webhook tooother metodi di avvio di un runbook in [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Informazioni dettagliate sui webhook
Hello nella tabella seguente vengono descritte hello proprietà che devono essere configurati per un webhook.

| Proprietà | Descrizione |
|:--- |:--- |
| Nome |È possibile specificare qualsiasi nome desiderato per un webhook poiché si tratta di non esposti toohello client.  Viene utilizzato solo per si tooidentify hello runbook in automazione di Azure. <br>  Come procedura consigliata, è necessario assegnare un nome toohello correlati client che verrà usato hello webhook. |
| URL |URL Hello del webhook hello è l'indirizzo di hello univoco che un client chiama con un runbook di hello toostart HTTP POST collegata toohello webhook.  Viene generato automaticamente quando si crea hello webhook.  Non è possibile specificare un URL personalizzato. <br> <br>  Hello URL contiene un token di sicurezza che consente di hello runbook toobe richiamato da un sistema di terze parti con alcuna ulteriore autenticazione. Per questo motivo, deve essere considerato come una password.  Per motivi di sicurezza, è possibile solo hello di visualizzazione che URL nel portale di Azure all'indirizzo hello ora hello webhook hello viene creato. Si noti hello URL in un luogo sicuro per un utilizzo futuro. |
| Expiration date |Analogamente a un certificato, un webhook ha una data di scadenza oltre la quale non può più essere usato.  Dopo aver creato il webhook hello, è possibile modificare la data di scadenza. |
| Enabled |Un webhook viene abilitato per impostazione predefinita nel momento in cui viene creato.  Se si imposta la proprietà tooDisabled, quindi nessun client sarà in grado di toouse è.  È possibile impostare hello **abilitato** proprietà quando si creano hello webhook o in qualsiasi momento una volta viene creata. |

### <a name="parameters"></a>parameters
Un webhook è possibile definire i valori per parametri del runbook vengono utilizzati quando runbook hello viene avviata da quel webhook. Hello webhook deve includere i valori per eventuali parametri obbligatori di hello runbook e possono includere valori per i parametri facoltativi. Un webhook tooa valore configurato di parametro può essere modificato anche dopo aver creato webhoook hello. Più webhook collegati tooa singolo runbook può utilizzare valori di parametro diversi.

Quando un client avvia un runbook tramite un webhook, è possibile eseguire l'override di valori di parametro hello definiti in webhook hello.  dati tooreceive dal client di hello, hello runbook può accettare un singolo parametro chiamato **$WebhookData** di tipo [object] contenenti dati che il client hello include nella richiesta POST hello.

![Proprietà Webhookdata](media/automation-webhooks/webhook-data-properties.png)

Hello **$WebhookData** oggetto avrà hello le proprietà seguenti:

| Proprietà | Descrizione |
|:--- |:--- |
| WebhookName |nome Hello del webhook hello. |
| RequestHeader |Tabella hash contenente hello intestazioni della richiesta POST in arrivo hello. |
| RequestBody |corpo Hello della richiesta POST in arrivo hello.  Manterrà tutta la formattazione, ad esempio stringa, JSON, XML o dati codificati in un form. Hello runbook deve essere scritto toowork con formato dati hello previsto. |

Nessuna configurazione di prova webhook obbligatorio toosupport prova **$WebhookData** parametro e hello runbook non è necessario tooaccept è.  Se il runbook hello non definisce il parametro hello, i dettagli della richiesta di hello inviati dal client hello viene ignorato.

Se si specifica un valore per $WebhookData quando si crea il webhook hello, tale valore sarà sottoposta a override all'avvio hello webhook hello runbook con i dati hello richiesta POST di hello del client, anche se hello client non include tutti i dati nel corpo della richiesta hello.  Se si avvia un runbook con $WebhookData utilizzando un metodo diverso da un webhook, è possibile fornire un valore per $Webhookdata che verrà riconosciuto dal runbook hello.  Questo valore deve essere un oggetto con hello stesso [proprietà](#details-of-a-webhook) come $Webhookdata runbook hello poter lavorare correttamente con esso, come se ha lavorato con WebhookData effettivo passato da un webhook.

Ad esempio, se si inizia hello seguente runbook dal portale di Azure hello e si desidera toopass alcuni WebhookData di esempio per test, perché WebhookData è un oggetto, deve essere passata come JSON in hello dell'interfaccia utente.

![Parametro WebhookData dall'interfaccia utente](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Per hello sopra runbook, se si dispone delle seguenti proprietà per il parametro WebhookData hello hello:

1. WebhookName: *MyWebhook*
2. RequestHeader: *From=Test User*
3. RequestBody: *[“VM1”, “VM2”]*

Passare quindi hello il valore JSON in hello dell'interfaccia utente per il parametro WebhookData hello seguente:  

* {"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}

![Parametro WebhookData Start dall'interfaccia utente](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> i valori Hello di tutti i parametri di input vengono registrati con il processo di runbook hello.  Ciò significa che qualsiasi input fornito dal client hello nella richiesta webhook hello sarà tooanyone registrati e disponibili con il processo di automazione toohello di accesso.  Per questo motivo è consigliabile procedere con cautela quando si includono dati sensibili nelle chiamate di webhook.
>

## <a name="security"></a>Sicurezza
sicurezza di Hello di un webhook si basa su privacy hello del relativo URL che contiene un token di sicurezza che ne consenta toobe richiamato. Automazione di Azure non esegue alcuna autenticazione sulla richiesta di hello fino a quando viene reso toohello URL sia corretto. Per questo motivo, webhook non devono essere utilizzati per i runbook che eseguono funzioni estremamente riservate senza utilizzare un metodo alternativo di convalida richiesta hello.

È possibile includere logica all'interno di hello toodetermine di runbook che è stato chiamato da un webhook controllando hello **WebhookName** proprietà del parametro hello $WebhookData. Hello runbook potrebbe eseguire un'ulteriore convalida mediante la ricerca di particolari informazioni di hello **RequestHeader** o **RequestBody** proprietà.

Un'altra strategia consiste toohave hello runbook eseguire una convalida di una condizione di esterna quando ricevuta una richiesta di webhook.  Ad esempio, si consideri un runbook che viene chiamato da GitHub tutte le volte che un nuovo repository GitHub tooa di commit.  Hello runbook potrebbero connettersi toovalidate tooGitHub che il commit di una nuova semplicemente si è verificato prima di continuare.

## <a name="creating-a-webhook"></a>Creazione di un webhook
Utilizzare hello seguendo procedure toocreate un nuovo runbook tooa webhook collegati in hello portale di Azure.

1. Da hello **pannello runbook** hello portale di Azure, fare clic su runbook hello hello webhook inizierà tooview il pannello di dettaglio.
2. Fare clic su **Webhook** nella parte superiore di hello di hello di hello pannello tooopen **Webhook aggiungere** blade. <br>
   ![Pulsante Webhook](media/automation-webhooks/webhooks-button.png)
3. Fare clic su **creare nuovo webhook** tooopen hello **crea webhook pannello**.
4. Specificare un **nome**, **data di scadenza** per webhook hello e se deve essere abilitata. Per altre informazioni su queste proprietà, vedere [Informazioni dettagliate sui webhook](#details-of-a-webhook) .
5. Fare clic sull'icona di copia hello e premere Ctrl + C toocopy hello URL del webhook hello.  Annotarlo in un luogo sicuro.  **Dopo aver creato il webhook hello, è possibile recuperare nuovamente hello URL.** <br>
   ![URL webhook](media/automation-webhooks/copy-webhook-url.png)
6. Fare clic su **parametri** tooprovide valori per parametri del runbook hello.  Se il runbook di hello include i parametri obbligatori, quindi non sarà in grado di toocreate hello webhook a meno che non vengono forniti i valori.
7. Fare clic su **crea** toocreate hello webhook.

## <a name="using-a-webhook"></a>Uso di un webhook
toouse un webhook dopo che è stato creato, l'applicazione client deve eseguire un POST HTTP con hello URL per il webhook hello.  sintassi di Hello del webhook hello sarà nel seguente formato hello.

    http://<Webhook Server>/token?=<Token Value>

Hello client riceverà uno dei seguenti codici restituiti da una richiesta POST hello hello.  

| Codice | Testo | Descrizione |
|:--- |:--- |:--- |
| 202 |Accepted |è stata accettata la richiesta di Hello e hello runbook è stato accodato correttamente. |
| 400 |Bad Request |richiesta di Hello non è stata accettata per uno dei seguenti motivi hello. <ul> <li>Hello webhook è scaduto.</li> <li>Hello webhook è disabilitata.</li> <li>token Hello hello URL è valido.</li>  </ul> |
| 404 |Non trovato |richiesta di Hello non è stata accettata per uno dei seguenti motivi hello. <ul> <li>Hello webhook non è stato trovato.</li> <li>Hello runbook non è stato trovato.</li> <li>Impossibile trovare l'account di Hello.</li>  </ul> |
| 500 |Internal Server Error |Hello URL è valido, ma si è verificato un errore.  Inviare nuovamente la richiesta hello. |

Supponendo che hello richiesta ha esito positivo, hello webhook risposta contiene come indicato di seguito id processo hello in formato JSON. Contiene un id di processo, ma il formato JSON hello consente per possibili miglioramenti futuri.

    {"JobIds":["<JobId>"]}  

Hello client non può determinare quando viene completato il processo di runbook hello o lo stato di completamento da hello webhook.  È possibile determinare queste informazioni utilizzando l'id di processo hello con un altro metodo, ad esempio [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) o hello [API di automazione di Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Esempio
Hello di esempio seguente viene utilizzato Windows PowerShell toostart un runbook con un webhook.  Si noti che qualsiasi linguaggio in grado di creare una richiesta HTTP può usare un webhook. Windows PowerShell viene usato qui solo come esempio.

runbook Hello è previsto un elenco di macchine virtuali in formato JSON nel corpo di hello di hello richiesta. È inoltre incluso informazioni che è l'avvio di runbook hello e hello data e l'ora viene avviato nell'intestazione hello hello richiesta.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Hello figura seguente vengono illustrate le informazioni di intestazione hello (utilizzando un [Fiddler](http://www.telerik.com/fiddler) traccia) dalla richiesta. Sono incluse le intestazioni standard di una richiesta HTTP in aggiunta toohello data personalizzato e da intestazioni che è stato aggiunto.  Ognuno di questi valori è runbook toohello disponibile in hello **RequestHeaders** proprietà di **WebhookData**.

![Pulsante Webhooks](media/automation-webhooks/webhook-request-headers.png)

Hello immagine seguente viene illustrato hello corpo della richiesta di hello (utilizzando un [Fiddler](http://www.telerik.com/fiddler) traccia) che è disponibile toohello runbook hello **RequestBody** proprietà di **WebhookData**. Questo è formattato come JSON, perché questo è il formato hello che è stato incluso nel corpo di hello di hello richiesta.     

![Pulsante Webhooks](media/automation-webhooks/webhook-request-body.png)

Hello immagine seguente mostra la richiesta di hello inviata da Windows PowerShell e la risposta risultante hello.  id di processo Hello viene estratto dalla risposta hello e stringa tooa convertito.

![Pulsante Webhooks](media/automation-webhooks/webhook-request-response.png)

Hello runbook di esempio seguente accetta una richiesta di esempio precedente hello e avvia le macchine virtuali hello specificate nel corpo della richiesta hello.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>A partire da runbook avvisi tooAzure risposta
Abilitato Webhook runbook può essere utilizzato tooreact troppo[gli avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Le risorse in Azure possono essere monitorate tramite la raccolta di statistiche hello come prestazioni, disponibilità e utilizzo con l'aiuto di hello degli avvisi di Azure. È possibile ricevere avvisi basati su metriche o eventi di monitoraggio per i servizi di Azure, attualmente gli account di automazione supportano solo le metriche. Quando il valore di hello di una specifica metrica supera la soglia di hello assegnata o se hello configurato evento viene generato una notifica viene inviata toohello servizio amministratore o co-amministratori tooresolve hello avviso, per ulteriori informazioni sulle metriche e gli eventi, vedere troppo[ Gli avvisi di Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Oltre a utilizzare gli avvisi di Azure come un sistema di notifica, è possibile anche avviare i runbook in risposta tooalerts. Automazione di Azure fornisce hello funzionalità toorun abilitato webhook runbook con gli avvisi di Azure. Quando una metrica supera hello configurato il valore di soglia hello regola di avviso diventa attiva e trigger hello webhook di automazione che a sua volta esegue hello runbook.

![Webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Contesto dell'avviso
Si consideri una risorsa di Azure, ad esempio una macchina virtuale, utilizzo della CPU del computer è uno della metrica di prestazioni chiave hello. Utilizzo della CPU hello è 100% o più di una certa quantità per lunghi periodi di tempo, è possibile problema hello toofix di toorestart hello macchina virtuale. Questo può essere risolto configurando una macchina virtuale toohello di regola di avviso e questa regola ha la percentuale di CPU come la metrica. Percentuale CPU qui viene eseguita solo come esempio, ma sono disponibili molte altre metriche che è possibile configurare tooyour Azure risorse e riavvio della macchina virtuale hello è un'azione che viene eseguita toofix questo problema, è possibile configurare hello runbook tootake altre azioni.

Quando la regola di avviso hello diventa attiva e trigger hello abilitato webhook runbook, invia hello al contesto dell'avviso toohello runbook. [Contesto dell'avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contiene i dettagli inclusi **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** e **Timestamp** che sono necessari per la risorsa di hello runbook tooidentify hello in cui in corso azione. Avviso di contesto è incorporato nella parte corpo hello di hello **WebhookData** oggetto runbook toohello inviato e sono accessibili con **Webhook.RequestBody** proprietà

### <a name="example"></a>Esempio
Creare una macchina virtuale di Azure nella sottoscrizione e associare un [avviso metriche Percentuale CPU toomonitor](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Durante la creazione avviso hello assicurarsi che inserire hello webhook campo hello URL del webhook hello generato durante la creazione del webhook hello.

runbook di esempio seguente Hello viene generato quando la regola di avviso hello diventa attiva e raccoglie i parametri di contesto dell'avviso hello che sono necessari per la risorsa di hello runbook tooidentify hello in cui in corso azione.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Passaggi successivi
* Per informazioni su modi toostart un runbook, vedere [avvio di un Runbook](automation-starting-a-runbook.md).
* Per informazioni sulla visualizzazione hello stato di un Runbook Job, vedere troppo[esecuzione di Runbook in automazione di Azure](automation-runbook-execution.md).
* toolearn toouse azione tootake di automazione di Azure per gli avvisi di Azure, vedere [correggere gli avvisi di macchina virtuale di Azure con i runbook di automazione](automation-azure-vm-alert-integration.md).
