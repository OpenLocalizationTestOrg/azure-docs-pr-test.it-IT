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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Monitorare i gateway VPN con la risoluzione dei problemi di Network Watcher

Ottenere informazioni complete sulle prestazioni di rete è toocustomers servizi affidabili tooprovide critici. È pertanto critico toodetect condizioni di interruzione della rete rapidamente e richiedere una condizione di interruzione di un'azione correttiva toomitigate hello. Automazione di Azure consente tooimplement ed esegue un'attività in modo a livello di codice i runbook. Con Automazione di Azure è possibile mettere in atto una soluzione continua e attiva di monitoraggio e avviso relativa alla rete.

## <a name="scenario"></a>Scenario

uno scenario Hello hello seguente immagine è un'applicazione a più livelli, con connettività locale stabilita utilizzando un Gateway VPN e tunnel. Assicurando hello che gateway VPN sia attivo e in esecuzione è delle prestazioni di applicazioni critiche toohello.

Un runbook viene creato con un toocheck di script per lo stato di connessione del tunnel VPN hello, utilizzando hello API di risoluzione dei problemi di risorse toocheck tunnel lo stato della connessione. Se lo stato di hello non è integro, un trigger di posta elettronica viene inviato tooadministrators.

![Esempio dello scenario][scenario]

Questo scenario illustrerà come:

- Creare un hello chiamata runbook `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot lo stato di connessione
- Collega un runbook toohello pianificazione

## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare questo scenario, è necessario disporre di hello seguenti prerequisiti:

- Un account di automazione di Azure in Azure. Verificare che l'account di automazione hello sono moduli più recenti di hello e dispone anche di modulo AzureRM.Network hello. modulo AzureRM.Network Hello è disponibile nella raccolta di moduli hello se è necessario tooadd è tooyour account di automazione.
- Un set di credenziali configurato in Automazione di Azure. Per altre informazioni, vedere l'articolo relativo alla [sicurezza in Automazione di Azure](../automation/automation-security-overview.md).
- Un server SMTP valido, che sia di Office 365, della posta elettronica in locale o altro, e credenziali definite in Automazione di Azure.
- Un gateway di rete virtuale configurato in Azure.
- Un account di archiviazione esistente con un esistente hello toostore contenitore l'accesso.

> [!NOTE]
> infrastruttura Hello illustrato nell'immagine precedente hello è a scopo illustrativo e non vengono creati con i passaggi di hello contenuti in questo articolo.

### <a name="create-hello-runbook"></a>Creare runbook hello

esempio hello tooconfiguring Hello primo passaggio è toocreate hello runbook. Questo esempio usa un account RunAs. toolearn sugli account RunAs, visitare [runbook l'autenticazione con account RunAs di Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Passaggio 1

Passare tooAzure automazione in hello [portale di Azure](https://portal.azure.com) e fare clic su **runbook**

![Panoramica dell'account di Automazione][1]

### <a name="step-2"></a>Passaggio 2

Fare clic su **aggiungere un runbook** toostart processo di creazione hello di hello runbook.

![Pannello Runbook][2]

### <a name="step-3"></a>Passaggio 3

In **creazione rapida**, fare clic su **creare un nuovo runbook** toocreate hello runbook.

![Pannello Aggiungi runbook][3]

### <a name="step-4"></a>Passaggio 4

In questo passaggio è dare hello runbook un nome, nell'esempio hello viene chiamato **Get VPNGatewayStatus**. È importante toogive hello runbook un nome descrittivo e consiglia di assegnargli un nome che segue gli standard di denominazione standard di PowerShell. tipo di runbook Hello per questo esempio è **PowerShell**, hello sono altre opzioni di grafici, flusso di lavoro PowerShell e PowerShell con interfaccia grafica del flusso di lavoro.

![Pannello Runbook][4]

### <a name="step-5"></a>Passaggio 5

In questo passaggio hello runbook viene creato, hello esempio di codice seguente fornisce che tutti hello codice necessario per l'esempio hello. elementi di codice hello contenenti Hello \<valore\> necessario toobe sostituiti con i valori hello dalla sottoscrizione.

Esempio di codice seguente di hello utilizzare come fare clic su **salvare**

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

### <a name="step-6"></a>Passaggio 6

Dopo aver salvato, hello runbook una pianificazione deve essere collegato tooit tooautomate hello inizio hello runbook. processo di hello toostart, fare clic su **pianificazione**.

![Passaggio 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Collega un runbook toohello pianificazione

È necessario creare una nuova pianificazione. Fare clic su **collega un runbook tooyour pianificazione**.

![Passaggio 7][7]

### <a name="step-1"></a>Passaggio 1

In hello **pianificazione** pannello, fare clic su **creare una nuova pianificazione**

![Passaggio 8][8]

### <a name="step-2"></a>Passaggio 2

In hello **nuova pianificazione** compilazione pannello delle informazioni sulla pianificazione di hello. i valori di Hello che è possibile impostare sono in hello seguente elenco:

- **Nome** -nome descrittivo di hello della pianificazione di hello.
- **Descrizione** -una descrizione della pianificazione hello.
- **Avvia** -questo valore è una combinazione di data, ora e fuso orario che costituiscono i trigger di pianificazione di hello ora hello.
- **Ricorrenza** -questo valore determina la ripetizione di pianificazioni hello.  I valori validi sono **Una sola volta** o **Ricorrente**.
- **Ricorre ogni** -intervallo di ricorrenza hello di pianificazione di hello in ore, giorni, settimane o mesi.
- **Impostare la scadenza** -valore hello determina se la pianificazione hello deve scadere o non. È possibile impostare troppo**Sì** o **n**. Una data valida e un'ora sono toobe fornito se si sceglie Sì.

> [!NOTE]
> Se è necessario toohave un runbook eseguito più spesso di ogni ora, è necessario creare più pianificazioni a intervalli diversi (vale a dire, 15, 30, 45 minuti dopo ora hello)

![Passaggio 9:][9]

### <a name="step-3"></a>Passaggio 3

Fare clic su Salva toosave hello pianificazione toohello runbook.

![Passaggio 10][10]

## <a name="next-steps"></a>Passaggi successivi

Ora che è necessario comprendere la risoluzione dei problemi Watcher di rete toointegrate con automazione di Azure, informazioni su come acquisizioni di pacchetti tootrigger avvisi VM visitando [creare un'acquisizione di pacchetti generati avvisi con il Watcher di rete di Azure](network-watcher-alert-triggered-packet-capture.md).

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
