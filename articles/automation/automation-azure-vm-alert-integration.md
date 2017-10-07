---
title: aaa"correzione gli avvisi di macchina virtuale di Azure con i runbook di automazione | Documenti di Microsoft"
description: In questo articolo viene illustrato come macchina virtuale di Azure toointegrate avvisi con i runbook di automazione di Azure e correzione automaticamente problemi
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Scenario di Automazione di Azure: risolvere gli avvisi delle macchine virtuali di Azure
Automazione di Azure e macchine virtuali di Azure hanno rilasciato una nuova funzionalità che consentono di runbook di automazione toorun avvisi tooconfigure macchina virtuale (VM). Questa nuova funzionalità consente tooautomatically eseguire la correzione degli standard negli avvisi tooVM risposta, ad esempio il riavvio o arresto hello macchina virtuale.

In precedenza, durante la creazione della regola di avviso di macchina virtuale è stato possibile troppo[specificare un webhook di automazione](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook nell'ordine toorun hello runbook ogni volta che ha attivato l'avviso hello. Tuttavia, questo richiede il lavoro hello toodo di creazione di runbook hello creazione hello webhook per runbook hello e quindi copiare e incollare hello webhook durante la creazione della regola di avviso. Con questa nuova versione, il processo di hello è molto più semplice poiché è possibile scegliere un runbook direttamente da un elenco durante la creazione della regola di avviso e, è possibile scegliere un account di automazione per l'esecuzione di runbook hello o creare facilmente un account.

In questo articolo verrà illustrato come è facile tooset impostare un avviso di macchina virtuale di Azure e configurata un' toorun runbook di automazione ogni volta che l'avviso hello attiva. Scenari di esempio includono il riavvio di una macchina virtuale quando l'utilizzo di memoria hello supera una determinata soglia di scadenza tooan applicazione hello macchina virtuale con una perdita di memoria o l'arresto di una macchina virtuale quando tempo utente hello della CPU è rimasto di sotto % 1 per ora precedente e non è in uso. Spiega anche come hello automatizzata la creazione di un'entità servizio nell'automazione account semplifica l'utilizzo di hello di runbook in Azure monitoraggio e aggiornamento degli avvisi.

## <a name="create-an-alert-on-a-vm"></a>Creare un avviso in una VM
Eseguire hello seguendo i passaggi tooconfigure un avviso toolaunch un runbook quando la soglia è stata soddisfatta.

> [!NOTE]
> Con questa versione sono supportate solo le macchine virtuali V2, mentre il supporto per le VM classiche verrà aggiunto a breve.  
> 
> 

1. Accedi toohello portale di Azure e fare clic su **macchine virtuali**.  
2. Selezionare una macchina virtuale.  Hello pannello dashboard macchina virtuale verrà visualizzato e hello **impostazioni** destra tooits blade.  
3. Da hello **impostazioni** pannello, hello selezionare sezione monitoraggio **regole di avviso**.
4. In hello **regole di avviso** pannello, fare clic su **Aggiungi avviso**.

Verrà visualizzata hello **aggiungere una regola di avviso** pannello, in cui è possibile configurare le condizioni di hello per avviso hello e scegliere tra una o tutte queste opzioni: inviare posta elettronica toosomeone, utilizzare un sistema di avviso tooanother webhook tooforward hello, e/o eseguire un runbook di automazione problema hello tooremediate tentativo di risposta.

## <a name="configure-a-runbook"></a>Configurare un runbook
tooconfigure toorun un runbook quando viene raggiunta la soglia di avviso di hello macchina virtuale, selezionare **Runbook di automazione**. In hello **Configura runbook** pannello, è possibile selezionare hello toorun di runbook e runbook hello automazione account toorun hello in.

![Configurare un runbook di automazione e creare un nuovo account di automazione](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Per questa versione è possibile scegliere tra tre runbook che fornisce il servizio hello-VM riavviare, arrestare VM o macchina virtuale rimuovere (eliminare).  Hello possibilità tooselect altri runbook o uno dei propri runbook sarà disponibile nelle versioni future.
> 
> 

![I runbook toochoose da](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Dopo aver selezionato uno dei runbook disponibili hello tre, hello **account di automazione** viene visualizzato l'elenco a discesa ed è possibile selezionare un'automazione runbook hello account verrà eseguito. I runbook necessario toorun nel contesto di hello di un [account di automazione](automation-security-overview.md) che si trova in una sottoscrizione di Azure. È possibile selezionare un account di automazione già creato o crearne automaticamente uno nuovo.

i runbook Hello forniti autenticare tooAzure usando un'entità servizio. Se si sceglie toorun hello runbook in uno degli account di automazione esistente, si creerà automaticamente servizio hello principale per l'utente. Se si sceglie toocreate un nuovo account di automazione, quindi verrà automaticamente creata account hello e dell'entità servizio hello. In entrambi i casi, le attività verranno inoltre create nell'account di automazione: un asset del certificato denominato hello **AzureRunAsCertificate** e un asset della connessione denominata **AzureRunAsConnection**. i runbook Hello useranno **AzureRunAsConnection** tooauthenticate con Azure nell'azione di gestione di ordine tooperform hello contro hello macchina virtuale.

> [!NOTE]
> entità servizio Hello viene creato nell'ambito della sottoscrizione hello e viene assegnato il ruolo di collaboratore hello. Questo ruolo è necessario affinché hello account toohave autorizzazione toorun automazione runbook toomanage macchine virtuali di Azure.  creazione di Hello di un account Automaton e/o l'entità servizio è un evento singolo. Una volta creati, è possibile utilizzare i runbook toorun tale account per gli altri avvisi macchina virtuale di Azure.
> 
> 

Quando fa clic su **OK** avviso hello è configurato e se si seleziona l'opzione di hello toocreate un nuovo account di automazione, viene creato insieme a un'entità servizio hello.  Questa operazione può richiedere alcuni secondi toocomplete.  

![Runbook in corso di configurazione](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Dopo aver completata la configurazione hello verrà visualizzato il nome di hello di hello runbook vengono visualizzate in hello **aggiungere una regola di avviso** blade.

![Runbook configurati](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Fare clic su **OK** in hello **aggiungere una regola di avviso** blade e hello regola di avviso verrà creato e attivato se macchina virtuale hello è in esecuzione.

### <a name="enable-or-disable-a-runbook"></a>Abilitare o disabilitare un runbook
Se si dispone di un runbook configurato per un avviso, è possibile disabilitarlo senza rimuovere la configurazione di runbook hello. Questo consente avviso hello tookeep in esecuzione e provare ad esempio hello regole di avviso e quindi in un secondo momento abilitare nuovamente hello runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Creare un runbook che funzioni con un avviso di Azure
Quando si sceglie un runbook come parte di una regola di avviso di Azure, hello runbook deve logica toohave toomanage hello dati di avviso che viene passati tooit.  Quando un runbook è configurato in una regola di avviso, viene creato un webhook hello runbook. tale webhook è utilizzato toostart hello runbook ogni trigger avviso hello di tempo.  Hello chiamata effettiva toostart hello runbook è un URL del webhook toohello richiesta HTTP POST. corpo Hello della richiesta POST hello contiene un oggetto formattato con JSON che contiene l'avviso correlati toohello proprietà utili.  Come può vedere di seguito, i dati di avviso hello contengono dettagli come ID sottoscrizione, resourceGroupName, resourceName e resourceType.

### <a name="example-of-alert-data"></a>Esempio di dati di avviso
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Quando hello servizio webhook di automazione riceve hello HTTP POST estrae i dati di avviso hello e passa toohello runbook nel parametro di input di hello WebhookData runbook.  Di seguito è riportato un runbook di esempio che illustra come toouse WebhookData parametro hello ed estrarre i dati di avviso hello e usarlo hello toomanage risorse di Azure che ha attivato hello avviso.

### <a name="example-runbook"></a>Runbook di esempio
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Riepilogo
Quando si configura un avviso in una macchina virtuale di Azure, è ora possibile configurare un'automazione hello possibilità tooeasily runbook tooautomatically eseguire l'azione di correzione quando genera l'avviso hello. Per questa versione, è possibile scegliere tra i runbook toorestart, arrestare o eliminare una macchina virtuale a seconda dello scenario di avviso. È sufficiente hello avvio dell'abilitazione di scenari in cui controllare le azioni di hello (notifica, risoluzione dei problemi, monitoraggio e aggiornamento) che verranno eseguite automaticamente quando si attiva un avviso.

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
* toolearn ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)

