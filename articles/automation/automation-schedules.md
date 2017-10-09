---
title: aaaSchedules in automazione di Azure | Documenti Microsoft
description: "Le pianificazioni di automazione vengono utilizzati tooschedule runbook in automazione di Azure toostart automaticamente. Viene descritto come toocreate e gestire una pianificazione in modo che è possibile avviare automaticamente un runbook in un momento specifico o in una pianificazione ricorrente."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Pianificazione di un runbook in Automazione di Azure
tooschedule un runbook in automazione di Azure toostart a un'ora specificata, è necessario collegarlo tooone o più pianificazioni. Una pianificazione può essere configurato tooeither eseguito una volta o in un record ogni ora o pianificazione giornaliera per i runbook nel portale di Azure classico hello e per i runbook hello portale di Azure, è inoltre possibile pianificare tali per settimanali, mensili, specifici giorni della settimana hello o i giorni di hello mese o un determinato giorno del mese hello.  Un runbook può essere collegato toomultiple pianificazioni e una pianificazione può includere più runbook collegati tooit.

> [!NOTE]
> Le pianificazioni attualmente non supportano le configurazioni DSC di automazione di Azure.
> 
> 

## <a name="windows-powershell-cmdlets"></a>Cmdlet di Windows PowerShell
cmdlet Hello in hello nella tabella seguente sono utilizzati toocreate e gestire le pianificazioni con Windows PowerShell in automazione di Azure. Vengono forniti come parte di hello [modulo Azure PowerShell](/powershell/azure/overview).

| Cmdlet | Descrizione |
|:--- |:--- |
| **Cmdlet di Azure Resource Manager** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |Recupera una pianificazione. |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |Crea una nuova pianificazione. |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |Rimuove una pianificazione. |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |Imposta le proprietà di hello per una pianificazione esistente. |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |Recupera i runbook pianificati. |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |Associa un runbook a una pianificazione. |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |Annulla l'associazione di un runbook a una pianificazione. |
| **Cmdlet di gestione dei servizi di Azure** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |Recupera una pianificazione. |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |Crea una nuova pianificazione. |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |Rimuove una pianificazione. |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |Imposta le proprietà di hello per una pianificazione esistente. |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Recupera i runbook pianificati. |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Associa un runbook a una pianificazione. |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |Annulla l'associazione di un runbook a una pianificazione. |

## <a name="creating-a-schedule"></a>Creazione di una pianificazione
È possibile creare una nuova pianificazione per i runbook nel portale di Azure hello nel portale classico hello o con Windows PowerShell. È anche possibile hello di creazione di una nuova pianificazione quando si collega una pianificazione del runbook tooa utilizzando hello Azure classico o il portale di Azure.

> [!NOTE]
> Quando viene eseguito un nuovo processo pianificato, automazione di Azure utilizzerà i moduli più recenti di hello nell'account di automazione.  conseguenze per i runbook e hello tooavoid processi automatizzare, è innanzitutto consigliabile testare tutti i runbook che sono collegate le pianificazioni con un account di automazione dedicato per il test.  Convaliderà programmate runbook continuano toowork correttamente e se non è possibile un'ulteriore risoluzione dei problemi e applicare eventuali modifiche necessarie prima di eseguire la migrazione tooproduction versione del runbook hello aggiornato.  
>  L'account di automazione non avranno automaticamente eventuali nuove versioni dei moduli a meno che non sono aggiornate manualmente selezionando hello [i moduli di Azure Update](automation-update-azure-modules.md) opzione hello **moduli** blade. 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>una nuova pianificazione nel portale di Azure hello toocreate
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **asset** riquadro tooopen hello **asset** blade.
2. Fare clic su hello **pianificazioni** riquadro tooopen hello **pianificazioni** blade.
3. Fare clic su **aggiungere una pianificazione** nella parte superiore di hello del pannello hello.
4. In hello **nuova pianificazione** pannello, digitare un **nome** e facoltativamente un **descrizione** per la nuova pianificazione hello.
5. Selezionare se pianificazione hello verrà eseguita una sola volta o in una pianificazione ricorrente selezionando **una volta** o **ricorrenza**.  Se si seleziona **Una sola volta** specificare un'**Ora di inizio** e quindi fare clic su **Crea**.  Se si seleziona **ricorrenza**, specificare un **ora di inizio** e la frequenza di hello per la frequenza con cui toorepeat runbook hello - da **ora**, **giorno**, **settimana**, o da **mese**.  Se si seleziona **settimana** o **mese** dall'elenco a discesa hello, hello **opzione relativa alla ricorrenza** verranno visualizzati nel pannello hello e dopo la selezione, hello **ricorrenza opzione** pannello verrà visualizzato e se è selezionata, è possibile selezionare giorno hello della settimana **settimana**.  Se si seleziona **mese**, è possibile scegliere **giorni feriali** o specifici giorni del mese di hello in hello calendario e, infine, si desidera toorun sul hello ultimo giorno del mese hello o non e quindi fare clic su **OK** .   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>una nuova pianificazione nel portale di Azure classico hello toocreate
1. Nel portale di Azure classico hello, selezionare l'automazione e quindi selezionare il nome di hello di un account di automazione.
2. Seleziona hello **asset** scheda.
3. Nella parte inferiore di hello della finestra hello, fare clic su **Aggiungi impostazione**.
4. Fare clic su **Aggiungi pianificazione**.
5. Digitare un **nome** e facoltativamente un **descrizione** per schedule.your nuovo hello pianificazione verrà eseguita **una volta**, **oraria**, **Giornaliero**, **settimanale**, o **mensile**.
6. Specificare un **ora di inizio** e altre opzioni in base al tipo di hello di pianificazione selezionato.

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate una nuova pianificazione con Windows PowerShell
È possibile utilizzare hello [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) toocreate cmdlet una nuova pianificazione in automazione di Azure per i runbook classici, o [New AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet per i runbook hello Azure portale. È necessario specificare l'ora di inizio hello pianificazione hello e la frequenza di hello che deve essere eseguito.

Mostra i comandi di esempio seguente Hello come toocreate una pianificazione per hello 15 e 30 di ogni mese utilizzando un cmdlet di gestione risorse di Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

Hello comandi di esempio seguente mostra come toocreate una nuova pianificazione che viene eseguito ogni giorno alle 3:30 PM 20 gennaio 2015 partendo da un cmdlet di gestione dei servizi Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>Il collegamento di un runbook tooa pianificazione
Un runbook può essere collegato toomultiple pianificazioni e una pianificazione può includere più runbook collegati tooit. Se un runbook dispone di parametri, è possibile fornire valori per tali parametri. È necessario specificare i valori per tutti i parametri obbligatori, mentre è possibile scegliere se specificare o meno i valori per i parametri facoltativi.  Questi valori verranno utilizzati ogni volta hello runbook viene avviato per la pianificazione.  È possibile collegare hello stesso runbook tooanother pianificazione e specificare valori di parametro diversi.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink un runbook tooa pianificazione con hello portale di Azure
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **runbook** riquadro tooopen hello **runbook** blade.
2. Fare clic sul nome di hello di hello runbook tooschedule.
3. Se hello runbook non è attualmente collegato tooa pianificazione, quindi si intende hello determinata opzione toocreate una nuova pianificazione o collegare tooan pianificazione esistente.  
4. Se hello runbook include parametri, è possibile selezionare l'opzione hello **modificare le impostazioni di esecuzione (impostazione predefinita: Azure)** hello e **parametri** pannello viene visualizzato in cui è possibile immettere informazioni hello di conseguenza.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>un runbook tooa pianificazione con il portale di Azure classico hello toolink
1. Nel portale di Azure classico hello, selezionare **automazione** e quindi fare clic su nome hello di un account di automazione.
2. Seleziona hello **runbook** scheda.
3. Fare clic sul nome di hello di hello runbook tooschedule.
4. Fare clic su hello **pianificazione** scheda.
5. Se hello runbook non è attualmente collegato tooa pianificazione, l'utente potrà opzione hello troppo**collegamento tooa nuova pianificazione** o **collegamento tooan pianificazione esistente**.  Se runbook hello è attualmente collegato tooa pianificazione, fare clic su **collegamento** in hello fondo tooaccess finestra hello queste opzioni.
6. Se hello runbook include parametri, verrà richiesto per i relativi valori.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink un runbook tooa pianificazione con Windows PowerShell
È possibile utilizzare hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink un runbook di pianificazione tooa classico o [registro AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet per i runbook hello portale di Azure.  È possibile specificare valori per parametri del runbook hello con parametro parametri hello. Per altre informazioni su come specificare i valori dei parametri, vedere [Avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md) .

Mostra i comandi di esempio seguente Hello come toolink un runbook tooa pianificazione utilizzando un cmdlet di gestione risorse di Azure con parametri.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
Mostra i comandi di esempio seguente Hello come toolink una pianificazione utilizzando un cmdlet di gestione del servizio Azure con parametri.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>Disabilitazione di una pianificazione
Quando si disabilita una pianificazione, qualsiasi tooit runbook collegati non verranno più eseguite su tale pianificazione. È possibile disabilitare manualmente una pianificazione o impostare un'ora di scadenza per le pianificazioni con una frequenza durante la fase di creazione. Quando viene raggiunta l'ora di scadenza hello, hello pianificazione viene disabilitata.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable hello portale di Azure di una pianificazione
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **asset** riquadro tooopen hello **asset** blade.
2. Fare clic su hello **pianificazioni** riquadro tooopen hello **pianificazioni** blade.
3. Fare clic su nome hello di un pannello dettagli di pianificazione tooopen hello.
4. Modifica **abilitato** troppo**n**.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>una pianificazione dal portale di Azure classico hello toodisable
È possibile disabilitare una pianificazione nel portale di Azure classico dalla pagina dei dettagli della pianificazione hello per pianificazione hello hello.

1. Nel portale di Azure classico hello, selezionare automazione e quindi fare clic su nome hello di un account di automazione.
2. Selezionare hello asset scheda.
3. Fare clic su nome hello di tooopen una pianificazione relativa pagina di dettagli.
4. Modifica **abilitato** troppo**n**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable una pianificazione con Windows PowerShell
È possibile utilizzare hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) proprietà hello toochange di cmdlet di una pianificazione esistente per un runbook classico o [Set AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet per i runbook hello Azure portale. hello toodisable pianificare, specificare **false** per hello **IsEnabled** parametro.

Mostra i comandi di esempio seguente Hello come toodisable una pianificazione per un runbook utilizzando un cmdlet di gestione risorse di Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

Hello comandi di esempio seguente viene illustrato come una pianificazione utilizzando toodisable hello cmdlet di gestione del servizio Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook in automazione di Azure, vedere [avvio di un Runbook in automazione di Azure](automation-starting-a-runbook.md) 

