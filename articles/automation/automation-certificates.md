---
title: Asset di tipo certificato in Automazione di Azure | Documentazione Microsoft
description: I certificati possono essere archiviati in modo sicuro in Automazione di Azure, in modo che i runbook o le configurazioni DSC possano accedervi per eseguire l'autenticazione rispetto a risorse di Azure e di terze parti.  Questo articolo illustra nel dettaglio i certificati e spiega come usarli nella creazione testuale e grafica.
services: automation
documentationcenter: 
author: georgewallace
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2017
ms.author: magoedte;bwren
ms.openlocfilehash: b6a5ff4fa3fd0084fd910968651c6ae0fefaf2cf
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Asset di tipo certificato in Automazione di Azure

I certificati possono essere archiviati in modo sicuro in Automazione di Azure, in modo che vi possano accedere i runbook o le configurazioni DSC che usano l'attività **Get-AzureRmAutomationCertificate** per le risorse di Azure Resource Manager. Ciò permette di creare runbook e configurazioni DSC che usano certificati per l'autenticazione o di aggiungerli a risorse di Azure o di terze parti.

> [!NOTE] 
> Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate. Questi asset vengono crittografati e archiviati in Automazione di Azure tramite una chiave univoca generata per ogni account di automazione. La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure. Prima dell'archiviazione di un asset sicuro, la chiave per l'account di automazione viene decrittografata mediante il certificato master e viene quindi usata per crittografare l'asset.
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlet di Windows PowerShell

I cmdlet della tabella seguente vengono usati per creare e gestire asset di certificati di automazione con Windows PowerShell. Sono inclusi nel [modulo Azure PowerShell](../powershell-install-configure.md) , disponibile per l'uso nei runbook di Automazione e nelle configurazioni DSC.

|Cmdlets|DESCRIZIONE|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/get-azurermautomationcertificate?view=azurermps-4.3.1)|Recupera le informazioni su un certificato da usare in un runbook o in una configurazione DSC. È possibile recuperare solo il certificato stesso dall'attività Get-AutomationCertificate.|
|[New-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/new-azurermautomationcertificate?view=azurermps-4.3.1)|Crea un nuovo certificato in Automazione di Azure.|
[Remove-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/remove-azurermautomationcertificate?view=azurermps-4.3.1)|Rimuove un certificato da Automazione di Azure.|Crea un nuovo certificato in Automazione di Azure.
|[Set-AzureRmAutomationCertificate](https://docs.microsoft.com/powershell/module/azurerm.automation/set-azurermautomationcertificate?view=azurermps-4.3.1)|Imposta le proprietà per un certificato esistente, inclusi il caricamento del file del certificato e l'impostazione della password per un file con estensione pfx.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Carica un certificato di servizio per il servizio cloud specificato.|


## <a name="python2-functions"></a>Funzioni Python2

La funzione nella tabella seguente viene usata per accedere ai certificati in un runbook Python2.

| Funzione | DESCRIZIONE |
|:---|:---|
| automationassets.get_automation_certificate | Recupera informazioni su un asset certificato. |

> [!NOTE]
> È necessario importare il modulo **automationassets** all'inizio del runbook Python per poter accedere alle funzioni dell'asset.


## <a name="creating-a-new-certificate"></a>Creazione di un nuovo certificato

Quando si crea un nuovo certificato, si carica un file con estensione cer o pfx in Automazione di Azure. Se si contrassegna il certificato come esportabile, sarà possibile trasferirlo all'esterno dell'archivio di certificati di Automazione di Azure. Se non è esportabile, sarà possibile usarlo solo per la firma entro il runbook o configurazione DSC.


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a>Per creare un nuovo certificato con il portale di Azure

1. Dall'account di automazione fare clic sul riquadro **Asset** per aprire il pannello **Asset**.
1. Fare clic sul riquadro **Certificati** per aprire il pannello **Certificati**.
1. Fare clic su **Aggiungi certificato** nella parte superiore del pannello.
2. Digitare un nome per il certificato nella casella **Nome** .
2. Fare clic su **Selezionare un file** in **Carica un file di certificato** per cercare un file con estensione cer o pfx.  Se si seleziona un file con estensione pfx, specificare una password e indicare se ne deve essere consentita l'esportazione.
1. Fare clic su **Crea** per salvare il nuovo asset di certificato.


### <a name="to-create-a-new-certificate-with-windows-powershell"></a>Per creare un nuovo certificato con Windows PowerShell

L'esempio che segue mostra come creare un nuovo certificato di automazione e come contrassegnarlo come esportabile. Verrà importato un file con estensione pfx esistente.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Utilizzo di un certificato

Per usare un certificato è necessario usare l'attività **Get-AutomationCertificate** . Non è possibile usare il cmdlet [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx), poiché restituisce informazioni sull'asset di certificato, ma non il certificato stesso.

### <a name="textual-runbook-sample"></a>Esempio di Runbook testuale

Il codice di esempio seguente mostra come aggiungere un certificato a un servizio cloud in un Runbook. In questo esempio la password viene recuperata da una variabile di automazione crittografata.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Esempio di Runbook grafico

Per aggiungere un'attività **Get-AutomationCertificate** a un runbook grafico, fare clic con il pulsante destro del mouse sul certificato nel riquadro della libreria dell'editor grafico e scegliere **Aggiungi ad area di disegno**.

![Aggiungere il certificato all'area di disegno](media/automation-certificates/automation-certificate-add-to-canvas.png)

La figura seguente mostra un esempio dell'uso di un certificato in un runbook grafico.  Si tratta dello stesso esempio mostrato in precedenza per l'aggiunta di un certificato a un servizio cloud da un runbook testuale.

![Esempio di creazione grafica ](media/automation-certificates/graphical-runbook-add-certificate.png)

### <a name="python2-sample"></a>Esempio Python2
L'esempio seguente illustra come accedere ai certificati nei runbook Python2.

    # get a reference to the Azure Automation certificate
    cert = automationassets.get_automation_certificate("AzureRunAsCertificate")
    
    # returns the binary cert content  
    print cert 

## <a name="next-steps"></a>Passaggi successivi

- Per ulteriori informazioni sull'utilizzo di collegamenti per controllare il flusso logico delle attività per le quali è progettato il runbook, vedere [Collegamenti nella creazione grafica](automation-graphical-authoring-intro.md#links-and-workflow). 
