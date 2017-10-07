---
title: gateway VPN aaaMonitor con la risoluzione dei problemi di controllo di rete di Azure | Documenti Microsoft
description: "Questo articolo illustra come diagnosticare la connettività locale con Automazione di Azure e Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="6acac-103">Monitorare i gateway VPN con la risoluzione dei problemi di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6acac-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="6acac-104">Ottenere informazioni complete sulle prestazioni di rete è toocustomers servizi affidabili tooprovide critici.</span><span class="sxs-lookup"><span data-stu-id="6acac-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="6acac-105">È pertanto critico toodetect condizioni di interruzione della rete rapidamente e richiedere una condizione di interruzione di un'azione correttiva toomitigate hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="6acac-106">Automazione di Azure consente tooimplement ed esegue un'attività in modo a livello di codice i runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="6acac-107">Con Automazione di Azure è possibile mettere in atto una soluzione continua e attiva di monitoraggio e avviso relativa alla rete.</span><span class="sxs-lookup"><span data-stu-id="6acac-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="6acac-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="6acac-108">Scenario</span></span>

<span data-ttu-id="6acac-109">uno scenario Hello hello seguente immagine è un'applicazione a più livelli, con connettività locale stabilita utilizzando un Gateway VPN e tunnel.</span><span class="sxs-lookup"><span data-stu-id="6acac-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="6acac-110">Assicurando hello che gateway VPN sia attivo e in esecuzione è delle prestazioni di applicazioni critiche toohello.</span><span class="sxs-lookup"><span data-stu-id="6acac-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="6acac-111">Un runbook viene creato con un toocheck di script per lo stato di connessione del tunnel VPN hello, utilizzando hello API di risoluzione dei problemi di risorse toocheck tunnel lo stato della connessione.</span><span class="sxs-lookup"><span data-stu-id="6acac-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="6acac-112">Se lo stato di hello non è integro, un trigger di posta elettronica viene inviato tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="6acac-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Esempio dello scenario][scenario]

<span data-ttu-id="6acac-114">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="6acac-114">This scenario will:</span></span>

- <span data-ttu-id="6acac-115">Creare un hello chiamata runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot lo stato di connessione</span><span class="sxs-lookup"><span data-stu-id="6acac-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="6acac-116">Collega un runbook toohello pianificazione</span><span class="sxs-lookup"><span data-stu-id="6acac-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6acac-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6acac-117">Before you begin</span></span>

<span data-ttu-id="6acac-118">Prima di iniziare questo scenario, è necessario disporre di hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="6acac-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="6acac-119">Un account di automazione di Azure in Azure.</span><span class="sxs-lookup"><span data-stu-id="6acac-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="6acac-120">Verificare che l'account di automazione hello sono moduli più recenti di hello e dispone anche di modulo AzureRM.Network hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="6acac-121">modulo AzureRM.Network Hello è disponibile nella raccolta di moduli hello se è necessario tooadd è tooyour account di automazione.</span><span class="sxs-lookup"><span data-stu-id="6acac-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="6acac-122">Un set di credenziali configurato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6acac-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="6acac-123">Per altre informazioni, vedere l'articolo relativo alla [sicurezza in Automazione di Azure](../automation/automation-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6acac-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="6acac-124">Un server SMTP valido, che sia di Office 365, della posta elettronica in locale o altro, e credenziali definite in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6acac-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="6acac-125">Un gateway di rete virtuale configurato in Azure.</span><span class="sxs-lookup"><span data-stu-id="6acac-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="6acac-126">Un account di archiviazione esistente con un esistente hello toostore contenitore l'accesso.</span><span class="sxs-lookup"><span data-stu-id="6acac-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="6acac-127">infrastruttura Hello illustrato nell'immagine precedente hello è a scopo illustrativo e non vengono creati con i passaggi di hello contenuti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6acac-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="6acac-128">Creare runbook hello</span><span class="sxs-lookup"><span data-stu-id="6acac-128">Create hello runbook</span></span>

<span data-ttu-id="6acac-129">esempio hello tooconfiguring Hello primo passaggio è toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="6acac-130">Questo esempio usa un account RunAs.</span><span class="sxs-lookup"><span data-stu-id="6acac-130">This example uses a run-as account.</span></span> <span data-ttu-id="6acac-131">toolearn sugli account RunAs, visitare [runbook l'autenticazione con account RunAs di Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="6acac-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="6acac-132">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="6acac-132">Step 1</span></span>

<span data-ttu-id="6acac-133">Passare tooAzure automazione in hello [portale di Azure](https://portal.azure.com) e fare clic su **runbook**</span><span class="sxs-lookup"><span data-stu-id="6acac-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Panoramica dell'account di Automazione][1]

### <a name="step-2"></a><span data-ttu-id="6acac-135">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="6acac-135">Step 2</span></span>

<span data-ttu-id="6acac-136">Fare clic su **aggiungere un runbook** toostart processo di creazione hello di hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![Pannello Runbook][2]

### <a name="step-3"></a><span data-ttu-id="6acac-138">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="6acac-138">Step 3</span></span>

<span data-ttu-id="6acac-139">In **creazione rapida**, fare clic su **creare un nuovo runbook** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Pannello Aggiungi runbook][3]

### <a name="step-4"></a><span data-ttu-id="6acac-141">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="6acac-141">Step 4</span></span>

<span data-ttu-id="6acac-142">In questo passaggio è dare hello runbook un nome, nell'esempio hello viene chiamato **Get VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="6acac-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="6acac-143">È importante toogive hello runbook un nome descrittivo e consiglia di assegnargli un nome che segue gli standard di denominazione standard di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6acac-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="6acac-144">tipo di runbook Hello per questo esempio è **PowerShell**, hello sono altre opzioni di grafici, flusso di lavoro PowerShell e PowerShell con interfaccia grafica del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6acac-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Pannello Runbook][4]

### <a name="step-5"></a><span data-ttu-id="6acac-146">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="6acac-146">Step 5</span></span>

<span data-ttu-id="6acac-147">In questo passaggio hello runbook viene creato, hello esempio di codice seguente fornisce che tutti hello codice necessario per l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="6acac-148">elementi di codice hello contenenti Hello \<valore\> necessario toobe sostituiti con i valori hello dalla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="6acac-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="6acac-149">Esempio di codice seguente di hello utilizzare come fare clic su **salvare**</span><span class="sxs-lookup"><span data-stu-id="6acac-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="6acac-150">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="6acac-150">Step 6</span></span>

<span data-ttu-id="6acac-151">Dopo aver salvato, hello runbook una pianificazione deve essere collegato tooit tooautomate hello inizio hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="6acac-152">processo di hello toostart, fare clic su **pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="6acac-152">toostart hello process, click **Schedule**.</span></span>

![Passaggio 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="6acac-154">Collega un runbook toohello pianificazione</span><span class="sxs-lookup"><span data-stu-id="6acac-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="6acac-155">È necessario creare una nuova pianificazione.</span><span class="sxs-lookup"><span data-stu-id="6acac-155">A new schedule must be created.</span></span> <span data-ttu-id="6acac-156">Fare clic su **collega un runbook tooyour pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="6acac-156">Click **Link a schedule tooyour runbook**.</span></span>

![Passaggio 7][7]

### <a name="step-1"></a><span data-ttu-id="6acac-158">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="6acac-158">Step 1</span></span>

<span data-ttu-id="6acac-159">In hello **pianificazione** pannello, fare clic su **creare una nuova pianificazione**</span><span class="sxs-lookup"><span data-stu-id="6acac-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Passaggio 8][8]

### <a name="step-2"></a><span data-ttu-id="6acac-161">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="6acac-161">Step 2</span></span>

<span data-ttu-id="6acac-162">In hello **nuova pianificazione** compilazione pannello delle informazioni sulla pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="6acac-163">i valori di Hello che è possibile impostare sono in hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="6acac-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="6acac-164">**Nome** -nome descrittivo di hello della pianificazione di hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="6acac-165">**Descrizione** -una descrizione della pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="6acac-166">**Avvia** -questo valore è una combinazione di data, ora e fuso orario che costituiscono i trigger di pianificazione di hello ora hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="6acac-167">**Ricorrenza** -questo valore determina la ripetizione di pianificazioni hello.</span><span class="sxs-lookup"><span data-stu-id="6acac-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="6acac-168">I valori validi sono **Una sola volta** o **Ricorrente**.</span><span class="sxs-lookup"><span data-stu-id="6acac-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="6acac-169">**Ricorre ogni** -intervallo di ricorrenza hello di pianificazione di hello in ore, giorni, settimane o mesi.</span><span class="sxs-lookup"><span data-stu-id="6acac-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="6acac-170">**Impostare la scadenza** -valore hello determina se la pianificazione hello deve scadere o non.</span><span class="sxs-lookup"><span data-stu-id="6acac-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="6acac-171">È possibile impostare troppo**Sì** o **n**.</span><span class="sxs-lookup"><span data-stu-id="6acac-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="6acac-172">Una data valida e un'ora sono toobe fornito se si sceglie Sì.</span><span class="sxs-lookup"><span data-stu-id="6acac-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="6acac-173">Se è necessario toohave un runbook eseguito più spesso di ogni ora, è necessario creare più pianificazioni a intervalli diversi (vale a dire, 15, 30, 45 minuti dopo ora hello)</span><span class="sxs-lookup"><span data-stu-id="6acac-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Passaggio 9:][9]

### <a name="step-3"></a><span data-ttu-id="6acac-175">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="6acac-175">Step 3</span></span>

<span data-ttu-id="6acac-176">Fare clic su Salva toosave hello pianificazione toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="6acac-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Passaggio 10][10]

## <a name="next-steps"></a><span data-ttu-id="6acac-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6acac-178">Next steps</span></span>

<span data-ttu-id="6acac-179">Ora che è necessario comprendere la risoluzione dei problemi Watcher di rete toointegrate con automazione di Azure, informazioni su come acquisizioni di pacchetti tootrigger avvisi VM visitando [creare un'acquisizione di pacchetti generati avvisi con il Watcher di rete di Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="6acac-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
