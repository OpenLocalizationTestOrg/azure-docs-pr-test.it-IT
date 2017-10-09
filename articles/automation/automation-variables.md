---
title: Asset aaaVariable in automazione di Azure | Documenti Microsoft
description: Gli asset variabili sono i valori disponibili tooall runbook e le configurazioni DSC in automazione di Azure.  In questo articolo vengono illustrati i dettagli di hello delle variabili e come toowork con essi in creazione grafica e testuale.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Asset di tipo variabile in Automazione di Azure

Gli asset variabili sono i valori disponibili tooall runbook e le configurazioni DSC nell'account di automazione. Può essere creati, modificati e recuperati dal hello portale di Azure, Windows PowerShell e da un runbook o una configurazione DSC. Le variabili di automazione sono utili per hello seguenti scenari:

- Condivisione di un valore tra più runbook o configurazioni DSC.

- Condividere un valore tra più processi da hello stesso runbook o la configurazione DSC.

- Gestire un valore dal portale hello o dalla riga di comando di Windows PowerShell hello utilizzato dal runbook o le configurazioni DSC, ad esempio un set comune di elementi di configurazione come elenco specifico di nomi di macchina virtuale, un gruppo di risorse specifico, un nome di dominio Active Directory e così via.  

Le variabili di automazione sono persistenti in modo da continuare toobe disponibile anche se il runbook hello o configurazione DSC non riesce.  Ciò consente anche di toobe un valore impostato da un runbook che viene quindi utilizzato da un altro, o da hello stesso runbook o hello configurazione DSC prossima volta che viene eseguito.

Quando si crea una variabile, è possibile specificare che venga archiviata in modalità crittografata.  Quando una variabile è crittografata, viene archiviato in modo sicuro in automazione di Azure e il relativo valore non è possibile recuperare da hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet fornito come parte del modulo Azure PowerShell hello.  Hello unico modo che sia possibile recuperare un valore crittografato è dall'hello **Get-AutomationVariable** attività in un runbook o di una configurazione DSC.

> [!NOTE]
> Gli asset sicuri in Automazione di Azure includono credenziali, certificati, connessioni e variabili crittografate. Questi asset vengono crittografati e archiviati in automazione di Azure con una chiave univoca generata per ogni account di automazione hello. La chiave viene crittografata da un certificato master e archiviata in Automazione di Azure. Prima di archiviare un bene sicuro, chiave hello per account di automazione hello viene decrittografato tramite certificato master hello e quindi asset hello tooencrypt.

## <a name="variable-types"></a>Tipi di variabile

Quando si crea una variabile con hello portale di Azure, è necessario specificare un tipo di dati dall'elenco a discesa hello in modo da portale hello può visualizzare controllo appropriato di hello per immettere il valore della variabile hello. la variabile di Hello non è limitato toothis dati tipo, ma è necessario impostare la variabile di hello tramite Windows PowerShell se si desidera toospecify un valore di un tipo diverso. Se si specifica **non definito**, quindi verrà impostato il valore di hello della variabile hello troppo**$null**, ed è necessario impostare il valore di hello con hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet o **Set-AutomationVariable** attività.  È possibile creare o modificare il valore di hello per un tipo di variabile complessa nel portale di hello, ma è possibile fornire un valore di qualsiasi tipo di utilizzo di Windows PowerShell. I tipi complessi verranno restituiti come [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

È possibile archiviare più singola variabile tooa valori mediante la creazione di una matrice o una tabella hash e salvandola toohello variabile.

di seguito Hello sono un elenco dei tipi di variabili disponibili in automazione di:

* String
* Integer
* DateTime
* Boolean
* Null

## <a name="cmdlets-and-workflow-activities"></a>Cmdlet e attività flusso di lavoro

cmdlet di Hello in hello nella tabella seguente vengono utilizzati toocreate e gestire le variabili di automazione con Windows PowerShell. Vengono forniti come parte di hello [modulo Azure PowerShell](../powershell-install-configure.md) che è possibile utilizzare nei runbook di automazione e la configurazione DSC.

|Cmdlet|Descrizione|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Recupera il valore di hello di una variabile esistente.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Crea una nuova variabile e ne imposta il valore.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Rimuove una variabile esistente.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Imposta il valore di hello per una variabile esistente.|

le attività del flusso di lavoro Hello in hello nella tabella seguente vengono utilizzati tooaccess le variabili di automazione in un runbook. Sono disponibili solo per l'utilizzo in un runbook o di una configurazione DSC e non vengono fornite come parte del modulo Azure PowerShell hello.

|Attività flusso di lavoro|Descrizione|
|:---|:---|
|Get-AutomationVariable|Recupera il valore di hello di una variabile esistente.|
|Set-AutomationVariable|Imposta il valore di hello per una variabile esistente.|

> [!NOTE] 
> È consigliabile evitare l'uso delle variabili nel hello – parametro Name di **Get-AutomationVariable** in un runbook o di una configurazione DSC, poiché ciò può complicare l'individuazione delle dipendenze tra i runbook o configurazione DSC e automazione variabili in fase di progettazione.

## <a name="creating-a-new-automation-variable"></a>Creazione di una nuova variabile di automazione

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate una nuova variabile con hello portale di Azure

1. Scegliere l'account di automazione, hello **asset** riquadro e quindi su hello **asset** pannello seleziona **variabili**.
2. In hello **variabili** riquadro, seleziona **aggiungere una variabile**.
3. Completare le opzioni di hello in hello **nuova variabile** pannello e fare clic su **crea** Salva hello nuova variabile.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate una nuova variabile con Windows PowerShell

Hello [New AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet crea una nuova variabile e imposta il valore iniziale. È possibile recuperare il valore hello utilizzando [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Se il valore di hello è un tipo semplice, viene restituito lo stesso tipo. Se è di tipo complesso, verrà restituito un **PSCustomObject** .

Mostra i comandi di esempio seguente Hello come toocreate una variabile di tipo stringa e restituirne il valore.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Mostra i comandi di esempio Hello seguente come una variabile con un oggetto complesso toocreate digitare e quindi restituire le relative proprietà. In questo caso, viene usato un oggetto macchina virtuale recuperato da **Get-AzureRmVm**.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Uso di una variabile in un Runbook o in una configurazione DSC

Hello utilizzare **Set-AutomationVariable** tooset hello valore dell'attività di una variabile di automazione in un runbook o una configurazione DSC e hello **Get-AutomationVariable** tooretrieve è.  È consigliabile utilizzare hello **Set-AzureAutomationVariable** o **Get-AzureAutomationVariable** cmdlet in una configurazione di DSC, perché sono meno efficiente dell'attività flusso di lavoro hello o un runbook.  È inoltre Impossibile recuperare il valore di hello delle variabili sicura con **Get-AzureAutomationVariable**.  Hello solo modo toocreate una variabile dall'interno di un runbook o configurazione di DSC è hello toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.


### <a name="textual-runbook-samples"></a>Esempi di runbook testuali

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Impostazione e recupero di un valore semplice da una variabile

Mostra i comandi di esempio seguente Hello come tooset e recuperare una variabile in un runbook testuale. In questo esempio si presuppone che siano già state create variabili di tipo integer denominate *NumberOfIterations* e *NumberOfRunnings* e una variabile di tipo stringa denominata *SampleMessage*.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Impostazione e recupero di un oggetto complesso in una variabile

Mostra codice di esempio seguente Hello come tooupdate una variabile con un valore complesso in un runbook testuale. In questo esempio, una macchina virtuale di Azure viene recuperata con **Get-AzureVM** e salvato tooan variabile di automazione esistente.  Come illustrato in [Tipi di variabile](#variable-types), viene archiviata come PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


Nel seguente codice di hello, il valore di hello viene recuperato dalla macchina virtuale di hello toostart variabile e usato hello.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Impostazione e recupero di una raccolta in una variabile

Mostra codice di esempio seguente Hello come toouse una variabile con una raccolta di valori complessi in un runbook testuale. In questo esempio, vengono recuperate più macchine virtuali di Azure con **Get-AzureVM** e salvato tooan variabile di automazione esistente.  Come illustrato in [Tipi di variabile](#variable-types), viene archiviata una raccolta di PSCustomObject.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

Nel seguente codice di hello, raccolta hello viene recuperato dalla variabile hello e utilizzato toostart ogni macchina virtuale.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Esempi di runbook grafici

In un runbook con interfaccia grafico, aggiungere hello **Get-AutomationVariable** o **Set-AutomationVariable** facendo clic sulla variabile hello nel riquadro libreria hello dell'editor grafico hello e selezionando hello attività desiderata.

![Aggiungere variabili toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Impostazione dei valori in una variabile
Hello immagine seguente mostra tooupdate le attività di esempio una variabile con un valore semplice in un runbook grafico. In questo esempio, una singola macchina virtuale di Azure viene recuperata con **Get AzureRmVM** e nome del computer hello salvata tooan variabile di automazione esistente con un tipo di stringa.  Non è rilevante se hello [collegamento è una pipeline o sequenza](automation-graphical-authoring-intro.md#links-and-workflow) poiché è probabile che solo un singolo oggetto nell'output di hello.

![Impostare una variabile semplice](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Passaggi successivi

* toolearn più sulla connessione delle attività tra loro in grafici per la modifica, vedere [collegamenti nella creazione di grafici](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md) 

