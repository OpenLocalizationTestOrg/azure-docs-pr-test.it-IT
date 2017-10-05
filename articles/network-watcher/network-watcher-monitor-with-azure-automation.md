---
title: Monitorare i gateway VPN con la risoluzione dei problemi di Azure Network Watcher | Microsoft Docs
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
ms.openlocfilehash: 55ec52dd0d94a0347cc67a8785b89611da955111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="00802-103">Monitorare i gateway VPN con la risoluzione dei problemi di Network Watcher</span><span class="sxs-lookup"><span data-stu-id="00802-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="00802-104">Ottenere informazioni approfondite sulle prestazioni di rete è fondamentale per offrire servizi affidabili ai clienti.</span><span class="sxs-lookup"><span data-stu-id="00802-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="00802-105">È quindi essenziale rilevare rapidamente le interruzioni di rete e adottare misure correttive per mitigare la condizione di interruzione.</span><span class="sxs-lookup"><span data-stu-id="00802-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="00802-106">Automazione di Azure consente di implementare ed eseguire un'attività a livello di codice attraverso i runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="00802-107">Con Automazione di Azure è possibile mettere in atto una soluzione continua e attiva di monitoraggio e avviso relativa alla rete.</span><span class="sxs-lookup"><span data-stu-id="00802-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="00802-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="00802-108">Scenario</span></span>

<span data-ttu-id="00802-109">Lo scenario nell'immagine seguente è un'applicazione a più livelli, con connettività locale stabilita tramite un gateway VPN e un tunnel.</span><span class="sxs-lookup"><span data-stu-id="00802-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="00802-110">Per prestazioni ottimali delle applicazioni è importante assicurarsi che il Gateway VPN sia in funzione.</span><span class="sxs-lookup"><span data-stu-id="00802-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="00802-111">Viene creato un runbook con uno script per il controllo dello stato della connessione del tunnel VPN, usando l'API di risoluzione dei problemi delle risorse per verificare lo stato della connessione del tunnel.</span><span class="sxs-lookup"><span data-stu-id="00802-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="00802-112">Se lo stato non è integro, viene inviato un trigger di posta elettronica agli amministratori.</span><span class="sxs-lookup"><span data-stu-id="00802-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![Esempio dello scenario][scenario]

<span data-ttu-id="00802-114">Questo scenario illustrerà come:</span><span class="sxs-lookup"><span data-stu-id="00802-114">This scenario will:</span></span>

- <span data-ttu-id="00802-115">Creare un runbook chiamando il cmdlet `Start-AzureRmNetworkWatcherResourceTroubleshooting` per risolvere lo stato di connessione.</span><span class="sxs-lookup"><span data-stu-id="00802-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="00802-116">Collegare una pianificazione al runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="00802-117">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="00802-117">Before you begin</span></span>

<span data-ttu-id="00802-118">Prima di iniziare questo scenario, sono necessari i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="00802-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="00802-119">Un account di automazione di Azure in Azure.</span><span class="sxs-lookup"><span data-stu-id="00802-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="00802-120">Assicurarsi che l'account di automazione abbia i moduli più recenti e anche il modulo AzureRM.Network.</span><span class="sxs-lookup"><span data-stu-id="00802-120">Ensure that the automation account has the latest modules and also has the AzureRM.Network module.</span></span> <span data-ttu-id="00802-121">Il modulo AzureRM.Network è disponibile nella raccolta di moduli, se è necessario aggiungerlo all'account di automazione.</span><span class="sxs-lookup"><span data-stu-id="00802-121">The AzureRM.Network module is available in the module gallery if you need to add it to your automation account.</span></span>
- <span data-ttu-id="00802-122">Un set di credenziali configurato in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00802-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="00802-123">Per altre informazioni, vedere l'articolo relativo alla [sicurezza in Automazione di Azure](../automation/automation-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="00802-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="00802-124">Un server SMTP valido, che sia di Office 365, della posta elettronica in locale o altro, e credenziali definite in Automazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="00802-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="00802-125">Un gateway di rete virtuale configurato in Azure.</span><span class="sxs-lookup"><span data-stu-id="00802-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="00802-126">Un account di archiviazione esistente con un contenitore esistente in cui archiviare i log.</span><span class="sxs-lookup"><span data-stu-id="00802-126">An existing storage account with an existing container to store the logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="00802-127">L'infrastruttura mostrata nell'immagine precedente è a scopo illustrativo e non è stata creata con la procedura descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="00802-127">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="00802-128">Creare il runbook</span><span class="sxs-lookup"><span data-stu-id="00802-128">Create the runbook</span></span>

<span data-ttu-id="00802-129">Il primo passaggio per la configurazione dell'esempio consiste nel creare il runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-129">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="00802-130">Questo esempio usa un account RunAs.</span><span class="sxs-lookup"><span data-stu-id="00802-130">This example uses a run-as account.</span></span> <span data-ttu-id="00802-131">Per altre informazioni sugli account RunAs, vedere [Autenticare runbook con account RunAs di Azure](../automation/automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="00802-131">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="00802-132">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="00802-132">Step 1</span></span>

<span data-ttu-id="00802-133">Passare ad Automazione di Azure nel [portale di Azure](https://portal.azure.com) e fare clic su **Runbook**.</span><span class="sxs-lookup"><span data-stu-id="00802-133">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Panoramica dell'account di Automazione][1]

### <a name="step-2"></a><span data-ttu-id="00802-135">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="00802-135">Step 2</span></span>

<span data-ttu-id="00802-136">Fare clic su **Aggiungi runbook** per avviare il processo di creazione del runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-136">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![Pannello Runbook][2]

### <a name="step-3"></a><span data-ttu-id="00802-138">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="00802-138">Step 3</span></span>

<span data-ttu-id="00802-139">In **Creazione rapida** fare clic su **Crea un nuovo runbook** per creare il runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-139">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![Pannello Aggiungi runbook][3]

### <a name="step-4"></a><span data-ttu-id="00802-141">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="00802-141">Step 4</span></span>

<span data-ttu-id="00802-142">In questo passaggio si attribuisce un nome al runbook, che nell'esempio è denominato **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="00802-142">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="00802-143">È importante attribuire al runbook un nome descrittivo che segua gli standard di denominazione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00802-143">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="00802-144">Il tipo di runbook per questo esempio è **PowerShell**, le altre opzioni disponibili sono Grafico, Flusso di lavoro PowerShell e Flusso di lavoro PowerShell grafico.</span><span class="sxs-lookup"><span data-stu-id="00802-144">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Pannello Runbook][4]

### <a name="step-5"></a><span data-ttu-id="00802-146">Passaggio 5</span><span class="sxs-lookup"><span data-stu-id="00802-146">Step 5</span></span>

<span data-ttu-id="00802-147">In questo passaggio viene creato il runbook. L'esempio di codice seguente contiene tutto il codice necessario per l'esempio.</span><span class="sxs-lookup"><span data-stu-id="00802-147">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="00802-148">Sostituire gli elementi nel codice che contengono \<value\> con i valori della sottoscrizione usata.</span><span class="sxs-lookup"><span data-stu-id="00802-148">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="00802-149">Usare il codice seguente e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="00802-149">Use the following code as click **Save**</span></span>

```PowerShell
# Set these variables to the proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<to email address>"
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

# Get the connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView the logs at $($storagePath) to learn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -To $toEmail `
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

### <a name="step-6"></a><span data-ttu-id="00802-150">Passaggio 6</span><span class="sxs-lookup"><span data-stu-id="00802-150">Step 6</span></span>

<span data-ttu-id="00802-151">Dopo aver salvato il runbook, è necessario collegarlo a una pianificazione per automatizzare l'avvio del runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-151">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="00802-152">Per avviare il processo, fare clic su **Pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="00802-152">To start the process, click **Schedule**.</span></span>

![Passaggio 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="00802-154">Collegare una pianificazione al runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-154">Link a schedule to the runbook</span></span>

<span data-ttu-id="00802-155">È necessario creare una nuova pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-155">A new schedule must be created.</span></span> <span data-ttu-id="00802-156">Fare clic su **Collegare una pianificazione al runbook**.</span><span class="sxs-lookup"><span data-stu-id="00802-156">Click **Link a schedule to your runbook**.</span></span>

![Passaggio 7][7]

### <a name="step-1"></a><span data-ttu-id="00802-158">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="00802-158">Step 1</span></span>

<span data-ttu-id="00802-159">Nel pannello **Pianificazione** fare clic su **Crea una nuova pianificazione**.</span><span class="sxs-lookup"><span data-stu-id="00802-159">On the **Schedule** blade, click **Create a new schedule**</span></span>

![Passaggio 8][8]

### <a name="step-2"></a><span data-ttu-id="00802-161">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="00802-161">Step 2</span></span>

<span data-ttu-id="00802-162">Nel pannello **Nuova pianificazione** immettere le informazioni sulla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-162">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="00802-163">Di seguito sono elencati i valori che è possibile impostare.</span><span class="sxs-lookup"><span data-stu-id="00802-163">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="00802-164">**Nome**: nome descrittivo della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-164">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="00802-165">**Descrizione**: descrizione della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-165">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="00802-166">**Inizia**: questo valore è una combinazione di data, ora e fuso orario che costituiscono l'orario di attivazione della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-166">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="00802-167">**Ricorrenza**: questo valore determina la ripetizione della pianificazione.</span><span class="sxs-lookup"><span data-stu-id="00802-167">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="00802-168">I valori validi sono **Una sola volta** o **Ricorrente**.</span><span class="sxs-lookup"><span data-stu-id="00802-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="00802-169">**Ricorre ogni**: intervallo di ricorrenza della pianificazione espresso in ore, giorni, settimane o mesi.</span><span class="sxs-lookup"><span data-stu-id="00802-169">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="00802-170">**Imposta scadenza**: questo valore determina se la pianificazione debba scadere o meno.</span><span class="sxs-lookup"><span data-stu-id="00802-170">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="00802-171">I valori validi sono **Sì** o **No**.</span><span class="sxs-lookup"><span data-stu-id="00802-171">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="00802-172">Sì è necessario specificare data e ora valide.</span><span class="sxs-lookup"><span data-stu-id="00802-172">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="00802-173">Se un runbook specifico deve essere eseguito con una frequenza superiore a un'ora, è necessario creare più pianificazioni a intervalli diversi, vale a dire a 15, 30, 45 minuti dopo l'ora.</span><span class="sxs-lookup"><span data-stu-id="00802-173">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![Passaggio 9:][9]

### <a name="step-3"></a><span data-ttu-id="00802-175">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="00802-175">Step 3</span></span>

<span data-ttu-id="00802-176">Fare clic su Salva per salvare la pianificazione del runbook.</span><span class="sxs-lookup"><span data-stu-id="00802-176">Click Save to save the schedule to the runbook.</span></span>

![Passaggio 10][10]

## <a name="next-steps"></a><span data-ttu-id="00802-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="00802-178">Next steps</span></span>

<span data-ttu-id="00802-179">Dopo aver appreso come integrare la risoluzione dei problemi di Network Watcher con Automazione di Azure, è possibile apprendere come attivare le acquisizioni pacchetti per gli avvisi di macchina virtuale. Vedere in proposito l'articolo relativo alla [creazione di un'acquisizione pacchetti attivata da un avviso mediante Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="00802-179">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
