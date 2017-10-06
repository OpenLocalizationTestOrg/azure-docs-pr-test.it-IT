---
title: Asset aaaConnection in automazione di Azure | Documenti Microsoft
description: Asset di connessione in automazione di Azure contiene servizio esterno tooan tooconnect informazioni necessarie hello o le applicazioni da un runbook o di una configurazione DSC. In questo articolo vengono illustrati i dettagli di hello di connessioni e come toowork con essi in creazione grafica e testuale.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Asset di connessione in Automazione di Azure

Un asset connessione di automazione contiene hello informazioni necessarie tooconnect tooan esterno servizio o applicazione da un runbook o di una configurazione DSC. Ciò può includere le informazioni necessarie per l'autenticazione, ad esempio un nome utente e una password informazioni tooconnection aggiuntive, ad esempio un URL o una porta. il valore di Hello di una connessione è mantenendo tutte le proprietà di hello di connessione particolare applicazione tooa in un asset, come toocreating anziché più variabili. utente Hello è possibile modificare i valori hello per una connessione in un'unica posizione, ed è possibile passare il nome di hello di una connessione tooa runbook o di una configurazione DSC in un singolo parametro. Hello proprietà per una connessione sono accessibili nel runbook hello o configurazione di DSC con hello **Get-AutomationConnection** attività.

Quando si crea una connessione, è necessario specificare un *tipo di connessione*. tipo di connessione Hello è un modello che definisce un set di proprietà. connessione Hello definisce valori per ogni proprietà definita nel relativo tipo di connessione. Tipi di connessione vengono aggiunti tooAzure automazione nei moduli di integrazione o creati con hello [API di automazione di Azure](http://msdn.microsoft.com/library/azure/mt163818.aspx) se il modulo di integrazione hello include un tipo di connessione e viene importato nell'account di automazione. In caso contrario, sarà necessario toocreate un toospecify di file di metadati un tipo di connessione di automazione.  Per ulteriori informazioni, vedere [Moduli di integrazione](automation-integration-modules.md).  

>[!NOTE] 
>Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate. Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello. La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure. Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.

## <a name="windows-powershell-cmdlets"></a>Cmdlet di Windows PowerShell

cmdlet Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire le connessioni di automazione con Windows PowerShell. Vengono forniti come parte di hello [modulo Azure PowerShell](/powershell/azure/overview) disponibile per l'uso nei runbook di automazione e le configurazioni DSC.

|Cmdlet|Descrizione|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Recupera una connessione. Include una tabella hash con i valori dei campi della connessione hello hello.|
|[New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Crea una nuova connessione.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Rimuove una connessione esistente.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Imposta il valore di hello di un campo specifico per una connessione esistente.|

## <a name="activities"></a>attività

le attività di Hello in hello nella tabella seguente sono connessioni tooaccess utilizzati in un runbook o di una configurazione DSC.

|attività|Descrizione|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Ottiene un toouse di connessione. Restituisce una tabella hash con proprietà hello della connessione di hello.|

>[!NOTE] 
>È consigliabile evitare l'utilizzo di variabili con hello – parametro Name di **Get - AutomationConnection** poiché ciò può complicare l'individuazione delle dipendenze tra i runbook o le configurazioni DSC e gli asset di connessione in fase di progettazione.

## <a name="creating-a-new-connection"></a>Creazione di una nuova connessione

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate una nuova connessione con hello portale di Azure

1. Scegliere l'account di automazione, hello **asset** parte tooopen hello **asset** blade.
2. Fare clic su hello **connessioni** parte tooopen hello **connessioni** blade.
3. Fare clic su **aggiungere una connessione** nella parte superiore di hello del pannello hello.
4. In hello **tipo** elenco a discesa Tipo selezionare hello di connessione desiderato toocreate. modulo Hello presenterà le proprietà di hello per quel determinato tipo.
5. Completare il modulo hello e fare clic su **crea** toosave hello nuova connessione.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate una nuova connessione con hello portale di Azure classico

1. Scegliere l'account di automazione, **asset** nella parte superiore di hello della finestra hello.
2. Nella parte inferiore di hello della finestra hello, fare clic su **Aggiungi impostazione**.
3. Fare clic su **Aggiungi connessione**.
4. In hello **tipo di connessione** elenco a discesa Tipo selezionare hello di connessione desiderato toocreate.  la procedura guidata Hello presenterà le proprietà di hello per quel determinato tipo.
5. Completare la procedura guidata hello e fare clic su hello casella di controllo toosave hello nuova connessione.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>toocreate una nuova connessione con Windows PowerShell

Creare una nuova connessione con Windows PowerShell usando hello [New AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet. Questo cmdlet ha un parametro denominato **ConnectionFieldValues** che prevede un [tabella hash](http://technet.microsoft.com/library/hh847780.aspx) che definisce i valori per ogni proprietà hello definiti dal tipo di connessione hello.

Se si ha familiarità con hello automazione [account RunAs](automation-sec-configure-azure-runas-account.md) tooauthenticate runbook usando l'entità servizio hello, hello fornito come un hello hello toocreating alternativo account RunAs dal portale di hello, lo script di PowerShell Crea un nuovo asset di connessione utilizzando i seguenti comandi di esempio hello.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Si è asset della connessione di toouse in grado di hello script toocreate hello perché quando si crea l'account di automazione, automaticamente include diversi moduli globali per impostazione predefinita con il tipo di connessione hello **AzurServicePrincipal**hello toocreate **AzureRunAsConnection** asset della connessione.  In questo modo tookeep importante ricordare, se si tenta un nuovo servizio tooa connessione asset tooconnect toocreate o un'applicazione con un metodo di autenticazione diversi, non riuscirà perché il tipo di connessione hello non è già definito nell'account di automazione.  Per ulteriori informazioni su come toocreate tipo di un tipo di connessione per la personalizzato o il modulo da hello [PowerShell Gallery](https://www.powershellgallery.com), vedere [moduli di integrazione](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Uso di una connessione in un Runbook o in una configurazione DSC

Recuperare una connessione in un runbook o di una configurazione DSC con hello **Get-AutomationConnection** cmdlet.  Non è possibile utilizzare hello [Get AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) attività.  Questa attività recupera i valori di hello di hello diversi campi nella connessione hello e li restituisce come una [tabella hash](http://go.microsoft.com/fwlink/?LinkID=324844) che può quindi essere usato con i comandi appropriati hello nel runbook hello o nella configurazione DSC.

### <a name="textual-runbook-sample"></a>Esempio di Runbook testuale

Hello comandi di esempio seguenti mostrano come toouse hello account Esegui come indicato in precedenza, tooauthenticate con risorse di gestione risorse di Azure nel runbook.  Usa connessione hello asset che rappresentano hello account RunAs, che fa riferimento a entità di servizio basata sui certificati di hello, non le credenziali.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Esempi di runbook grafici

Si aggiunge un **Get-AutomationConnection** runbook grafico tooa di attività facendo clic su connessione hello nel riquadro raccolta hello dell'editor grafico hello e selezionando **aggiungere toocanvas**.

![](media/automation-connections/connection-add-canvas.png)

Hello immagine seguente viene illustrato un esempio dell'utilizzo di una connessione in un runbook grafico.  Si tratta di hello stesso esempio illustrato in precedenza per l'autenticazione utilizzando l'account RunAs hello con un runbook testuale.  Questo esempio viene utilizzato hello **valore costante** set di dati per hello **ottenere connessione RunAs** attività che utilizza un oggetto di connessione per l'autenticazione.  Oggetto [collegamento alla pipeline](automation-graphical-authoring-intro.md#links-and-workflow) viene utilizzata in questo caso poiché hello ServicePrincipalCertificate set di parametri è previsto un singolo oggetto.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Passaggi successivi

- Revisione [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow) toounderstand funzionamento del flusso di controllo e toodirect hello della logica dei runbook.  

- toolearn più relative all'utilizzo di automazione di Azure i moduli di PowerShell e le procedure consigliate per la creazione di propri toowork moduli di PowerShell come moduli di integrazione in automazione di Azure, vedere [moduli di integrazione](automation-integration-modules.md).  
