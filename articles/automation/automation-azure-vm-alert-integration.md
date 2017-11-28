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
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="054e9-103">Scenario di Automazione di Azure: risolvere gli avvisi delle macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="054e9-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="054e9-104">Automazione di Azure e macchine virtuali di Azure hanno rilasciato una nuova funzionalità che consentono di runbook di automazione toorun avvisi tooconfigure macchina virtuale (VM).</span><span class="sxs-lookup"><span data-stu-id="054e9-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="054e9-105">Questa nuova funzionalità consente tooautomatically eseguire la correzione degli standard negli avvisi tooVM risposta, ad esempio il riavvio o arresto hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="054e9-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="054e9-106">In precedenza, durante la creazione della regola di avviso di macchina virtuale è stato possibile troppo[specificare un webhook di automazione](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook nell'ordine toorun hello runbook ogni volta che ha attivato l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="054e9-107">Tuttavia, questo richiede il lavoro hello toodo di creazione di runbook hello creazione hello webhook per runbook hello e quindi copiare e incollare hello webhook durante la creazione della regola di avviso.</span><span class="sxs-lookup"><span data-stu-id="054e9-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="054e9-108">Con questa nuova versione, il processo di hello è molto più semplice poiché è possibile scegliere un runbook direttamente da un elenco durante la creazione della regola di avviso e, è possibile scegliere un account di automazione per l'esecuzione di runbook hello o creare facilmente un account.</span><span class="sxs-lookup"><span data-stu-id="054e9-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="054e9-109">In questo articolo verrà illustrato come è facile tooset impostare un avviso di macchina virtuale di Azure e configurata un' toorun runbook di automazione ogni volta che l'avviso hello attiva.</span><span class="sxs-lookup"><span data-stu-id="054e9-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="054e9-110">Scenari di esempio includono il riavvio di una macchina virtuale quando l'utilizzo di memoria hello supera una determinata soglia di scadenza tooan applicazione hello macchina virtuale con una perdita di memoria o l'arresto di una macchina virtuale quando tempo utente hello della CPU è rimasto di sotto % 1 per ora precedente e non è in uso.</span><span class="sxs-lookup"><span data-stu-id="054e9-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="054e9-111">Spiega anche come hello automatizzata la creazione di un'entità servizio nell'automazione account semplifica l'utilizzo di hello di runbook in Azure monitoraggio e aggiornamento degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="054e9-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="054e9-112">Creare un avviso in una VM</span><span class="sxs-lookup"><span data-stu-id="054e9-112">Create an alert on a VM</span></span>
<span data-ttu-id="054e9-113">Eseguire hello seguendo i passaggi tooconfigure un avviso toolaunch un runbook quando la soglia è stata soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="054e9-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="054e9-114">Con questa versione sono supportate solo le macchine virtuali V2, mentre il supporto per le VM classiche verrà aggiunto a breve.</span><span class="sxs-lookup"><span data-stu-id="054e9-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="054e9-115">Accedi toohello portale di Azure e fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="054e9-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="054e9-116">Selezionare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="054e9-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="054e9-117">Hello pannello dashboard macchina virtuale verrà visualizzato e hello **impostazioni** destra tooits blade.</span><span class="sxs-lookup"><span data-stu-id="054e9-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="054e9-118">Da hello **impostazioni** pannello, hello selezionare sezione monitoraggio **regole di avviso**.</span><span class="sxs-lookup"><span data-stu-id="054e9-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="054e9-119">In hello **regole di avviso** pannello, fare clic su **Aggiungi avviso**.</span><span class="sxs-lookup"><span data-stu-id="054e9-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="054e9-120">Verrà visualizzata hello **aggiungere una regola di avviso** pannello, in cui è possibile configurare le condizioni di hello per avviso hello e scegliere tra una o tutte queste opzioni: inviare posta elettronica toosomeone, utilizzare un sistema di avviso tooanother webhook tooforward hello, e/o eseguire un runbook di automazione problema hello tooremediate tentativo di risposta.</span><span class="sxs-lookup"><span data-stu-id="054e9-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="054e9-121">Configurare un runbook</span><span class="sxs-lookup"><span data-stu-id="054e9-121">Configure a runbook</span></span>
<span data-ttu-id="054e9-122">tooconfigure toorun un runbook quando viene raggiunta la soglia di avviso di hello macchina virtuale, selezionare **Runbook di automazione**.</span><span class="sxs-lookup"><span data-stu-id="054e9-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="054e9-123">In hello **Configura runbook** pannello, è possibile selezionare hello toorun di runbook e runbook hello automazione account toorun hello in.</span><span class="sxs-lookup"><span data-stu-id="054e9-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Configurare un runbook di automazione e creare un nuovo account di automazione](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="054e9-125">Per questa versione è possibile scegliere tra tre runbook che fornisce il servizio hello-VM riavviare, arrestare VM o macchina virtuale rimuovere (eliminare).</span><span class="sxs-lookup"><span data-stu-id="054e9-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="054e9-126">Hello possibilità tooselect altri runbook o uno dei propri runbook sarà disponibile nelle versioni future.</span><span class="sxs-lookup"><span data-stu-id="054e9-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![I runbook toochoose da](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="054e9-128">Dopo aver selezionato uno dei runbook disponibili hello tre, hello **account di automazione** viene visualizzato l'elenco a discesa ed è possibile selezionare un'automazione runbook hello account verrà eseguito.</span><span class="sxs-lookup"><span data-stu-id="054e9-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="054e9-129">I runbook necessario toorun nel contesto di hello di un [account di automazione](automation-security-overview.md) che si trova in una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="054e9-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="054e9-130">È possibile selezionare un account di automazione già creato o crearne automaticamente uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="054e9-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="054e9-131">i runbook Hello forniti autenticare tooAzure usando un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="054e9-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="054e9-132">Se si sceglie toorun hello runbook in uno degli account di automazione esistente, si creerà automaticamente servizio hello principale per l'utente.</span><span class="sxs-lookup"><span data-stu-id="054e9-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="054e9-133">Se si sceglie toocreate un nuovo account di automazione, quindi verrà automaticamente creata account hello e dell'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="054e9-134">In entrambi i casi, le attività verranno inoltre create nell'account di automazione: un asset del certificato denominato hello **AzureRunAsCertificate** e un asset della connessione denominata **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="054e9-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="054e9-135">i runbook Hello useranno **AzureRunAsConnection** tooauthenticate con Azure nell'azione di gestione di ordine tooperform hello contro hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="054e9-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="054e9-136">entità servizio Hello viene creato nell'ambito della sottoscrizione hello e viene assegnato il ruolo di collaboratore hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="054e9-137">Questo ruolo è necessario affinché hello account toohave autorizzazione toorun automazione runbook toomanage macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="054e9-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="054e9-138">creazione di Hello di un account Automaton e/o l'entità servizio è un evento singolo.</span><span class="sxs-lookup"><span data-stu-id="054e9-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="054e9-139">Una volta creati, è possibile utilizzare i runbook toorun tale account per gli altri avvisi macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="054e9-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="054e9-140">Quando fa clic su **OK** avviso hello è configurato e se si seleziona l'opzione di hello toocreate un nuovo account di automazione, viene creato insieme a un'entità servizio hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="054e9-141">Questa operazione può richiedere alcuni secondi toocomplete.</span><span class="sxs-lookup"><span data-stu-id="054e9-141">This can take a few seconds toocomplete.</span></span>  

![Runbook in corso di configurazione](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="054e9-143">Dopo aver completata la configurazione hello verrà visualizzato il nome di hello di hello runbook vengono visualizzate in hello **aggiungere una regola di avviso** blade.</span><span class="sxs-lookup"><span data-stu-id="054e9-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Runbook configurati](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="054e9-145">Fare clic su **OK** in hello **aggiungere una regola di avviso** blade e hello regola di avviso verrà creato e attivato se macchina virtuale hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="054e9-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="054e9-146">Abilitare o disabilitare un runbook</span><span class="sxs-lookup"><span data-stu-id="054e9-146">Enable or disable a runbook</span></span>
<span data-ttu-id="054e9-147">Se si dispone di un runbook configurato per un avviso, è possibile disabilitarlo senza rimuovere la configurazione di runbook hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="054e9-148">Questo consente avviso hello tookeep in esecuzione e provare ad esempio hello regole di avviso e quindi in un secondo momento abilitare nuovamente hello runbook.</span><span class="sxs-lookup"><span data-stu-id="054e9-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="054e9-149">Creare un runbook che funzioni con un avviso di Azure</span><span class="sxs-lookup"><span data-stu-id="054e9-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="054e9-150">Quando si sceglie un runbook come parte di una regola di avviso di Azure, hello runbook deve logica toohave toomanage hello dati di avviso che viene passati tooit.</span><span class="sxs-lookup"><span data-stu-id="054e9-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="054e9-151">Quando un runbook è configurato in una regola di avviso, viene creato un webhook hello runbook. tale webhook è utilizzato toostart hello runbook ogni trigger avviso hello di tempo.</span><span class="sxs-lookup"><span data-stu-id="054e9-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="054e9-152">Hello chiamata effettiva toostart hello runbook è un URL del webhook toohello richiesta HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="054e9-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="054e9-153">corpo Hello della richiesta POST hello contiene un oggetto formattato con JSON che contiene l'avviso correlati toohello proprietà utili.</span><span class="sxs-lookup"><span data-stu-id="054e9-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="054e9-154">Come può vedere di seguito, i dati di avviso hello contengono dettagli come ID sottoscrizione, resourceGroupName, resourceName e resourceType.</span><span class="sxs-lookup"><span data-stu-id="054e9-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="054e9-155">Esempio di dati di avviso</span><span class="sxs-lookup"><span data-stu-id="054e9-155">Example of Alert data</span></span>
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

<span data-ttu-id="054e9-156">Quando hello servizio webhook di automazione riceve hello HTTP POST estrae i dati di avviso hello e passa toohello runbook nel parametro di input di hello WebhookData runbook.</span><span class="sxs-lookup"><span data-stu-id="054e9-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="054e9-157">Di seguito è riportato un runbook di esempio che illustra come toouse WebhookData parametro hello ed estrarre i dati di avviso hello e usarlo hello toomanage risorse di Azure che ha attivato hello avviso.</span><span class="sxs-lookup"><span data-stu-id="054e9-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="054e9-158">Runbook di esempio</span><span class="sxs-lookup"><span data-stu-id="054e9-158">Example runbook</span></span>
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

## <a name="summary"></a><span data-ttu-id="054e9-159">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="054e9-159">Summary</span></span>
<span data-ttu-id="054e9-160">Quando si configura un avviso in una macchina virtuale di Azure, è ora possibile configurare un'automazione hello possibilità tooeasily runbook tooautomatically eseguire l'azione di correzione quando genera l'avviso hello.</span><span class="sxs-lookup"><span data-stu-id="054e9-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="054e9-161">Per questa versione, è possibile scegliere tra i runbook toorestart, arrestare o eliminare una macchina virtuale a seconda dello scenario di avviso.</span><span class="sxs-lookup"><span data-stu-id="054e9-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="054e9-162">È sufficiente hello avvio dell'abilitazione di scenari in cui controllare le azioni di hello (notifica, risoluzione dei problemi, monitoraggio e aggiornamento) che verranno eseguite automaticamente quando si attiva un avviso.</span><span class="sxs-lookup"><span data-stu-id="054e9-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="054e9-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="054e9-163">Next Steps</span></span>
* <span data-ttu-id="054e9-164">tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="054e9-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="054e9-165">tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="054e9-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="054e9-166">toolearn ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="054e9-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

