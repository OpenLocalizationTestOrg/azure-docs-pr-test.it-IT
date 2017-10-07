---
title: Asset aaaCredential in automazione di Azure | Documenti Microsoft
description: Asset credenziali di automazione di Azure contengono le credenziali di sicurezza che possono essere utilizzati tooauthenticate tooresources accede runbook hello o configurazione DSC. In questo articolo viene descritto come toocreate asset delle credenziali e usarli in un runbook o di una configurazione DSC.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Asset credenziali in Automazione di Azure
Un asset credenziali di Automazione contiene un oggetto [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) contenente credenziali di sicurezza, ad esempio un nome utente e una password. Le configurazioni DSC e i runbook possono usare i cmdlet che accettano un oggetto PSCredential per l'autenticazione, o si può estrarre hello username e password dell'applicazione di toosome tooprovide oggetto PSCredential hello o un servizio che richiede l'autenticazione. proprietà Hello per le credenziali vengono archiviate in modo sicuro in automazione di Azure e sono accessibili nel runbook hello o configurazione di DSC con hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) attività.

> [!NOTE]
> Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate. Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello. La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure. Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.  

## <a name="windows-powershell-cmdlets"></a>Cmdlet di Windows PowerShell
cmdlet Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire asset credenziali di automazione con Windows PowerShell.  Vengono forniti come parte di hello [modulo Azure PowerShell](/powershell/azure/overview) disponibile per l'uso nei runbook di automazione e le configurazioni DSC.

| Cmdlet | Descrizione |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Recupera informazioni riguardo un asset credenziali. È possibile recuperare solo credenziali hello da **Get-AutomationPSCredential** attività. |
| [New-AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Crea nuove credenziali di Automazione. |
| [Remove- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Rimuove le credenziali di Automazione. |
| [Set- AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Set di hello le proprietà per le credenziali di automazione esistenti. |

## <a name="runbook-activities"></a>Attività del Runbook
le attività di Hello in hello nella tabella seguente sono utilizzati tooaccess credenziali in un runbook e le configurazioni DSC.

| attività | Descrizione |
|:--- |:--- |
| Get-AutomationPSCredential |Ottiene un toouse credenziali in un runbook o di una configurazione DSC. Restituisce un oggetto [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) . |

> [!NOTE]
> È consigliabile evitare l'uso delle variabili nel hello – parametro Name di Get-AutomationPSCredential poiché ciò può complicare l'individuazione delle dipendenze tra i runbook o le configurazioni DSC e asset delle credenziali in fase di progettazione.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Creazione di un nuovo asset credenziali

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate un nuovo asset delle credenziali con hello portale di Azure
1. Scegliere l'account di automazione, hello **asset** parte tooopen hello **asset** blade.
2. Fare clic su hello **credenziali** parte tooopen hello **credenziali** blade.
3. Fare clic su **aggiungere una credenziale** nella parte superiore di hello del pannello hello.
4. Completare il modulo hello e fare clic su **crea** toosave hello nuove credenziali.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate un nuovo asset delle credenziali con Windows PowerShell
Hello comandi di esempio seguenti mostrano come toocreate automazione un nuova credenziale. Un oggetto PSCredential viene innanzitutto creato con nome hello e una password e quindi utilizzato asset delle credenziali di hello toocreate. In alternativa, è possibile utilizzare hello **Get-Credential** toobe cmdlet richiesto tootype in un nome e una password.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate un nuovo asset delle credenziali con hello portale di Azure classico
1. Scegliere l'account di automazione, **asset** nella parte superiore di hello della finestra hello.
2. Nella parte inferiore di hello della finestra hello, fare clic su **Aggiungi impostazione**.
3. Fare clic su **Aggiungi credenziali**.
4. In hello **tipo di credenziale** elenco a discesa Seleziona **credenziale di PowerShell**.
5. Completare la procedura guidata hello e fare clic su hello casella di controllo toosave hello nuove credenziali.

## <a name="using-a-powershell-credential"></a>Uso di credenziali PowerShell 
Per recuperare un asset delle credenziali in un runbook o di una configurazione DSC con hello **Get-AutomationPSCredential** attività. Verrà restituito un [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) da usare con un'attività o un cmdlet che richiede un parametro PSCredential. È inoltre possibile recuperare le proprietà di hello di hello credenziali oggetto toouse singolarmente. oggetto Hello ha una proprietà per hello username e password sicura hello oppure è possibile utilizzare hello **GetNetworkCredential** metodo tooreturn un [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) oggetto che fornisce un non protetto versione della password hello.

### <a name="textual-runbook-sample"></a>Esempio di Runbook testuale
Hello comandi di esempio seguenti mostrano come toouse un PowerShell credenziali in un runbook. In questo esempio vengono recuperate credenziali hello e il nome utente e la password assegnata toovariables.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Esempio di Runbook grafico
Si aggiunge un **Get-AutomationPSCredential** runbook grafico tooa di attività facendo clic su credenziali hello nel riquadro libreria hello dell'editor grafico hello e selezionando **aggiungere toocanvas**.

![Aggiungere credenziali toocanvas](media/automation-credentials/credential-add-canvas.png)

Hello immagine seguente viene illustrato un esempio dell'utilizzo di una credenziale in un runbook grafico.  In questo caso, viene utilizzato tooprovide autenticazione per le risorse tooAzure un runbook come descritto in [runbook l'autenticazione con account utente di Active Directory di Azure](automation-create-aduser-account.md).  prima attività Hello recupera le credenziali di hello che ha accesso toohello sottoscrizione di Azure.  Hello **Add-AzureAccount** attività utilizza quindi tooprovide autenticazione delle credenziali per qualsiasi attività seguono.  Viene usato un [collegamento pipeline](automation-graphical-authoring-intro.md#links-and-workflow) poiché **Get-AutomationPSCredential** prevede un singolo oggetto.  

![Aggiungere credenziali toocanvas](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>Uso di credenziali PowerShell in DSC
Anche se le configurazioni DSC in Automazione di Azure possono fare riferimento ad asset credenziali con **Get-AutomationPSCredential**, gli asset credenziali possono essere passati anche con i parametri, se necessario. Per ulteriori informazioni vedere [Compilazione di configurazioni in Azure Automation DSC](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sui collegamenti nella creazione di grafici, vedere [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow)
* toounderstand hello diversi metodi di autenticazione con l'automazione, vedere [sicurezza di automazione di Azure](automation-security-overview.md)
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md) 

