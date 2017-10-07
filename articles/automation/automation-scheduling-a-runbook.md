---
title: aaaScheduling un runbook in automazione di Azure | Documenti Microsoft
description: "Viene descritto come toocreate una pianificazione in automazione di Azure in modo che è possibile avviare automaticamente un runbook in un momento specifico o in una pianificazione ricorrente."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a>Pianificazione di un runbook in Automazione di Azure
tooschedule un runbook in automazione di Azure toostart a un'ora specificata, è necessario collegarlo tooone o più pianificazioni. Una pianificazione può essere configurato tooeither eseguito una volta o scadenze ricorrente oraria o giornaliera per i runbook nel portale di Azure classico hello e per i runbook hello portale di Azure, è possibile inoltre programmarli per settimanali, mensili, specifici giorni della settimana hello o di giorni di mese Hello o un determinato giorno del mese hello.  Un runbook può essere collegato toomultiple pianificazioni e una pianificazione può includere più runbook collegati tooit.

## <a name="creating-a-schedule"></a>Creazione di una pianificazione
È possibile creare una nuova pianificazione per i runbook nel portale di Azure hello nel portale classico hello o con Windows PowerShell. È anche possibile hello di creazione di una nuova pianificazione quando si collega una pianificazione del runbook tooa utilizzando hello Azure classico o il portale di Azure.

> [!NOTE]
> Quando si associa una pianificazione a un runbook, automazione archivia le versioni correnti di hello dei moduli hello nell'account e li collega toothat pianificazione.  Ciò significa che se si dispone di un modulo con la versione 1.0 nell'account di durante la creazione di una pianificazione e quindi aggiornare hello modulo tooversion 2.0, pianificazione hello continuerà toouse 1.0.  Nella versione del modulo aggiornato hello toouse ordine, è necessario creare una nuova pianificazione. 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>una nuova pianificazione nel portale di Azure classico hello toocreate
1. Nel portale di Azure classico hello, selezionare automazione e quindi selezionare quindi il nome di hello di un account di automazione.
2. Seleziona hello **asset** scheda.
3. Nella parte inferiore di hello della finestra hello, fare clic su **Aggiungi impostazione**.
4. Fare clic su **Aggiungi pianificazione**.
5. Digitare un **nome** e facoltativamente un **descrizione** per schedule.your nuovo hello pianificazione verrà eseguita **una volta**, **oraria**, **Giornaliero**, **settimanale**, o **mensile**.
6. Specificare un **ora di inizio** e altre opzioni in base al tipo di hello di pianificazione selezionato.

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>una nuova pianificazione nel portale di Azure hello toocreate
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **asset** riquadro tooopen hello **asset** blade.
2. Fare clic su hello **pianificazioni** riquadro tooopen hello **pianificazioni** blade.
3. Fare clic su **aggiungere una pianificazione** nella parte superiore di hello del pannello hello.
4. In hello **nuova pianificazione** pannello, digitare un **nome** e facoltativamente un **descrizione** per la nuova pianificazione hello.
5. Selezionare se pianificazione hello verrà eseguita una sola volta o in una pianificazione ricorrente selezionando **una volta** o **ricorrenza**.  Se si seleziona **Una sola volta** specificare un'**Ora di inizio** e quindi fare clic su **Crea**.  Se si seleziona **ricorrenza**, specificare un **ora di inizio** e la frequenza di hello per la frequenza con cui toorepeat runbook hello - da **ora**, **giorno**, **settimana**, o da **mese**.  Se si seleziona **settimana** o **mese** dall'elenco a discesa hello, hello **opzione relativa alla ricorrenza** verranno visualizzati nel pannello hello e dopo la selezione, hello **ricorrenza opzione** pannello verrà visualizzato e se è selezionata, è possibile selezionare giorno hello della settimana **settimana**.  Se si seleziona **mese**, è possibile scegliere **giorni della settimana** o specifici giorni del mese di hello in hello calendario e, infine, si desidera toorun sul hello ultimo giorno del mese hello o non e quindi fare clic su **OK** .   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate una nuova pianificazione con Windows PowerShell
È possibile utilizzare hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) toocreate cmdlet una nuova pianificazione in automazione di Azure per i runbook classici, o [New AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet per i runbook hello Azure portale. È necessario specificare l'ora di inizio hello pianificazione hello e la frequenza di hello che deve essere eseguito.

Hello comandi di esempio seguente mostra come toocreate una nuova pianificazione che viene eseguito ogni giorno alle 3:30 PM 20 gennaio 2015 partendo da un cmdlet di gestione dei servizi Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

Hello seguente comandi Mostra come toocreate una pianificazione per hello 15 e 30 di ogni mese utilizzando un cmdlet di gestione risorse di Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>Il collegamento di un runbook tooa pianificazione
Un runbook può essere collegato toomultiple pianificazioni e una pianificazione può includere più runbook collegati tooit. Se un runbook dispone di parametri, è possibile fornire valori per tali parametri. È necessario specificare i valori per tutti i parametri obbligatori, mentre è possibile scegliere se specificare o meno i valori per i parametri facoltativi.  Questi valori verranno utilizzati ogni volta hello runbook viene avviato per la pianificazione.  È possibile collegare hello stesso runbook tooanother pianificazione e specificare valori di parametro diversi.

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>un runbook tooa pianificazione con il portale di Azure classico hello toolink
1. Nel portale di Azure classico hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.
2. Seleziona hello **runbook** scheda.
3. Fare clic sul nome di hello di hello runbook tooschedule.
4. Fare clic su hello **pianificazione** scheda.
5. Se hello runbook non è attualmente collegato tooa pianificazione, l'utente potrà opzione hello troppo**collegamento tooa nuova pianificazione** o **collegamento tooan pianificazione esistente**.  Se runbook hello è attualmente collegato tooa pianificazione, fare clic su **collegamento** in hello fondo tooaccess finestra hello queste opzioni.
6. Se hello runbook include parametri, verrà richiesto per i relativi valori.  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink un runbook tooa pianificazione con hello portale di Azure
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **runbook** riquadro tooopen hello **runbook** blade.
2. Fare clic sul nome di hello di hello runbook tooschedule.
3. Se hello runbook non è attualmente collegato tooa pianificazione, quindi si intende hello determinata opzione toocreate una nuova pianificazione o collegare tooan pianificazione esistente.  
4. Se hello runbook include parametri, è possibile selezionare l'opzione hello **modificare le impostazioni di esecuzione (impostazione predefinita: Azure)** hello e **parametri** pannello viene visualizzato in cui è possibile immettere informazioni hello di conseguenza.  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink un runbook tooa pianificazione con Windows PowerShell
È possibile utilizzare hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink un runbook di pianificazione tooa classico o [registro AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet per i runbook hello portale di Azure.  È possibile specificare valori per parametri del runbook hello con parametro parametri hello. Per altre informazioni su come specificare i valori dei parametri, vedere [Avvio di un runbook in Automazione di Azure](automation-starting-a-runbook.md) .

Mostra i comandi di esempio seguente Hello come toolink una pianificazione utilizzando un cmdlet di gestione del servizio Azure con parametri.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

Mostra i comandi di esempio seguente Hello come toolink un runbook tooa pianificazione utilizzando un cmdlet di gestione risorse di Azure con parametri.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>Disabilitazione di una pianificazione
Quando si disabilita una pianificazione, qualsiasi tooit runbook collegati non verranno più eseguite su tale pianificazione. È possibile disabilitare manualmente una pianificazione o impostare un'ora di scadenza per le pianificazioni con una frequenza durante la fase di creazione. Quando viene raggiunta l'ora di scadenza hello, hello pianificazione viene disabilitata.

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>una pianificazione dal portale di Azure classico hello toodisable
È possibile disabilitare una pianificazione nel portale di Azure classico dalla pagina dei dettagli della pianificazione hello per pianificazione hello hello.

1. Nel portale di Azure classico hello, selezionare automazione e quindi scegliere il nome di hello di un account di automazione.
2. Selezionare hello asset scheda.
3. Fare clic su nome hello di tooopen una pianificazione relativa pagina di dettagli.
4. Modifica **abilitato** troppo**n**.

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable hello portale di Azure di una pianificazione
1. Nel portale di Azure dall'account di automazione, hello fare clic su hello **asset** riquadro tooopen hello **asset** blade.
2. Fare clic su hello **pianificazioni** riquadro tooopen hello **pianificazioni** blade.
3. Fare clic su nome hello di un pannello dettagli di pianificazione tooopen hello.
4. Modifica **abilitato** troppo**n**.

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable una pianificazione con Windows PowerShell
È possibile utilizzare hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) proprietà hello toochange di cmdlet di una pianificazione esistente per un runbook classico o [Set AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet per i runbook hello Azure portale. hello toodisable pianificare, specificare **false** per hello **IsEnabled** parametro.

Hello comandi di esempio seguente viene illustrato come una pianificazione utilizzando toodisable hello cmdlet di gestione del servizio Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

Mostra i comandi di esempio seguente Hello come toodisable una pianificazione per un runbook utilizzando un cmdlet di gestione risorse di Azure.

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>Passaggi successivi
* toolearn più informazioni sull'utilizzo di pianificazioni, vedere [asset di pianificazione in automazione di Azure](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* tooget avviato con runbook in automazione di Azure, vedere [avvio di un Runbook in automazione di Azure](automation-starting-a-runbook.md) 

