---
title: Asset aaaCertificate in automazione di Azure | Documenti Microsoft
description: I certificati possono essere archiviati in modo sicuro in automazione di Azure in modo da renderli accessibili dal runbook o tooauthenticate configurazioni DSC da Azure e risorse di terze parti.  In questo articolo vengono illustrati i dettagli di hello dei certificati e come toowork con essi in creazione grafica e testuale.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a>Asset di tipo certificato in Automazione di Azure

I certificati possono essere archiviati in modo sicuro in automazione di Azure in modo da renderli accessibili dal runbook o delle configurazioni DSC tramite hello **Get AzureRmAutomationRmCertificate** attività per le risorse di gestione risorse di Azure. Questo consente toocreate runbook e le configurazioni DSC che utilizzano i certificati per l'autenticazione o li aggiunge risorse tooAzure o di terze parti.

> [!NOTE] 
> Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate. Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello. La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure. Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlet di Windows PowerShell

cmdlet Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire asset certificato di automazione con Windows PowerShell. Vengono forniti come parte di hello [modulo Azure PowerShell](../powershell-install-configure.md) disponibile per l'uso nei runbook di automazione e le configurazioni DSC.

|Cmdlet|Descrizione|
|:---|:---|
|[Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx)|Recupera informazioni su toouse un certificato in un runbook o di una configurazione DSC. È possibile recuperare solo il certificato hello stesso dall'attività Get-Automationcredential.|
|[New-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603604.aspx)|Crea un nuovo certificato in Automazione di Azure.|
[Remove-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603529.aspx)|Rimuove un certificato da Automazione di Azure.|Crea un nuovo certificato in Automazione di Azure.
|[Set-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603760.aspx)|Imposta le proprietà di hello per un certificato esistente, incluso il caricamento di file di certificato hello e impostazione password hello per un file pfx.|
|[Add-AzureCertificate](https://msdn.microsoft.com/library/azure/dn495214.aspx)|Caricamento di un servizio del certificato per hello specificato servizio cloud.|


## <a name="creating-a-new-certificate"></a>Creazione di un nuovo certificato

Quando si crea un nuovo certificato, caricare un tooAzure file con estensione cer o pfx automazione. Se si contrassegna certificato hello come esportabile, è possibile trasferirla dall'archivio certificati di automazione di Azure hello. Se non è esportabile, quindi può solo essere utilizzato per la firma all'interno di runbook hello o configurazione DSC.


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a>toocreate un nuovo certificato con hello portale di Azure

1. Scegliere l'account di automazione, hello **asset** riquadro tooopen hello **asset** blade.
1. Fare clic su hello **certificati** riquadro tooopen hello **certificati** blade.
1. Fare clic su **aggiungere un certificato** nella parte superiore di hello del pannello hello.
2. Digitare un nome per il certificato di hello hello **nome** casella.
2. Fare clic su **selezionare un file** in **caricare un file di certificato** toobrowse per un file con estensione cer o pfx.  Se si seleziona un file con estensione pfx, specificare una password e se che dovrebbe essere consentito toobe esportato.
1. Fare clic su **crea** toosave hello nuovo certificato asset.


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a>toocreate un nuovo certificato con Windows PowerShell

Hello esempio seguente viene illustrato come toocreate automazione un nuovo certificato e contrassegnarlo come esportabile. Verrà importato un file con estensione pfx esistente.

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a>Utilizzo di un certificato

È necessario utilizzare hello **Get-Automationcredential** attività toouse un certificato. Non è possibile utilizzare hello [Get AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet perché restituisce informazioni su asset del certificato di hello ma non certificato hello stesso.

### <a name="textual-runbook-sample"></a>Esempio di Runbook testuale

Hello seguente codice di esempio mostra come del cloud tooadd tooa un certificato di servizio in un runbook. In questo esempio, la password di hello viene recuperata dalla variabile di automazione crittografata.

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a>Esempio di Runbook grafico

Si aggiunge un **Get-Automationcredential** tooa runbook grafico facendo clic sul certificato hello nel riquadro libreria hello dell'editor grafico hello e selezionando **aggiungere toocanvas**.

![Aggiungere l'area di disegno toohello certificato](media/automation-certificates/automation-certificate-add-to-canvas.png)

Hello immagine seguente mostra un esempio di utilizzo di un certificato in un runbook grafico.  Si tratta di hello stesso esempio illustrato in precedenza per l'aggiunta di un servizio cloud tooa di certificato da un runbook testuale.

![Esempio di creazione grafica ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a>Passaggi successivi

- informazioni sull'utilizzo di collegamenti toocontrol hello un flusso logico delle attività del runbook è toolearn progettato tooperform, vedere [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow). 
