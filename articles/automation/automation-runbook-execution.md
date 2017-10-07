---
title: esecuzione di aaaRunbook in automazione di Azure | Documenti Microsoft
description: "Vengono descritti dettagliatamente hello della modalità di elaborazione di un runbook in automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Esecuzione di runbook in Automazione di Azure
Quando si avvia un runbook in Automazione di Azure, viene creato un processo. Un processo è una singola istanza di esecuzione di un runbook. Un thread di lavoro è di automazione di Azure assegnato toorun ogni processo. I computer di lavoro sono condivisi da più account Azure, mentre i processi di account di automazione diversi sono isolati l'uno dall'altro. Non si dispone del controllo sulla richiesta di hello servizi quali lavoro per il processo.  In un singolo runbook possono venire eseguiti più processi contemporaneamente. Quando si visualizza l'elenco di hello di runbook nel portale di Azure hello, elenca lo stato di hello di tutti i processi che sono stati avviati per ogni runbook. È possibile visualizzare l'elenco di hello di processi per ogni runbook in stato di ogni hello tootrack dell'ordine. Per una descrizione di hello diversi stati del processo, vedere [gli stati del processo](#job-statuses).

Hello diagramma seguente viene illustrato hello del ciclo di vita di un processo del runbook per [runbook grafici](automation-runbook-types.md#graphical-runbooks) e [runbook del flusso di lavoro di PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).

![Stati del processo - Flusso di lavoro PowerShell](./media/automation-runbook-execution/job-statuses.png)

Hello diagramma seguente viene illustrato hello del ciclo di vita di un processo del runbook per [runbook PowerShell](automation-runbook-types.md#powershell-runbooks).

![Stati del processo - Script PowerShell](./media/automation-runbook-execution/job-statuses-script.png)

I processi hanno accesso tooyour Azure risorse eseguendo un tooyour connessione sottoscrizione di Azure. Solo hanno accesso tooresources nel data center se tali risorse sono accessibili dal cloud pubblico hello.

## <a name="job-statuses"></a>Stati dei processi
Hello nella tabella seguente descrive hello diversi stati possibili per un processo.

| Stato | Descrizione |
|:--- |:--- |
| Completed |processo di Hello è stato completato. |
| Operazione non riuscita |Per [runbook grafici e flusso di lavoro PowerShell](automation-runbook-types.md), hello runbook non è stato possibile toocompile.  Per [runbook Script di PowerShell](automation-runbook-types.md), hello runbook non è stato possibile toostart o processo hello ha rilevato un'eccezione. |
| Failed, waiting for resources |Hello processo non riuscito perché ha raggiunto hello [condivisione equa](#fairshare) limitare a tre volte e avviato da hello stesso checkpoint o dall'hello ora di inizio del runbook hello ogni. |
| Queued |processo Hello è in attesa di risorse in un toocome di lavoro di automazione disponibili in modo che può essere avviato. |
| Avvio in corso |processo di Hello è stato assegnato il lavoro tooa e sistema hello è in corso di hello di avvio. |
| Resuming |sistema Hello è in corso di hello di riprendere il processo di hello dopo la sospensione. |
| In esecuzione |il processo di Hello è in esecuzione. |
| Running, waiting for resources |Hello processo è stato scaricato perché ha raggiunto hello [condivisione equa](#fairshare) limite. Riprende a breve dall'ultimo checkpoint. |
| Arrestato |il processo di Hello è stato arrestato dall'utente hello prima del completamento. |
| Arresto in corso |sistema Hello è in corso di hello di arrestare il processo di hello. |
| Suspended |il processo di Hello è stato sospeso dall'utente hello, dal sistema hello o da un comando nel runbook hello. Un processo sospeso può essere riavviato e ripreso dall'ultimo checkpoint o dall'inizio di hello di hello runbook se non dispone di checkpoint. Hello runbook verrà sospeso dal sistema hello solo quando si verifica un'eccezione. Per impostazione predefinita, ErrorActionPreference è troppo**continua**, vale a dire che il processo di hello rimangano in esecuzione in caso di errore. Se questa variabile di preferenza è impostata troppo**arrestare**, quindi sospende il processo di hello in caso di errore.  Si applica troppo[runbook grafici e flusso di lavoro PowerShell](automation-runbook-types.md) solo. |
| Suspending |sistema Hello sta tentando di processo hello toosuspend richiesta hello dell'utente hello. Hello runbook deve raggiungere il checkpoint successivo prima di poter essere sospeso. Se ha già superato l'ultimo checkpoint, il processo viene completato prima di poter essere sospeso.  Si applica troppo[runbook grafici e flusso di lavoro PowerShell](automation-runbook-types.md) solo. |

## <a name="viewing-job-status-from-hello-azure-portal"></a>Visualizzazione stato del processo da hello portale di Azure
È possibile visualizzare lo stato di riepilogo di tutti i processi runbook o esaminare i dettagli di un processo specifico del runbook nel portale di Azure hello o dalla configurazione dell'integrazione con lo stato del processo runbook tooforward dell'area di lavoro Analitica di Log di Microsoft Operations Management Suite (OMS) e flussi di lavoro.  Per ulteriori informazioni sull'integrazione con Analitica di Log di OMS, vedere [inoltra lo stato del processo e i flussi di lavoro da automazione tooLog Analitica (OMS)](automation-manage-send-joblogs-log-analytics.md).  

### <a name="automation-runbook-jobs-summary"></a>Riepilogo dei processi del Runbook di Automazione
In hello a destra dell'account di automazione selezionato, è possibile visualizzare un riepilogo di tutti i processi del runbook hello per un account di automazione selezionato in **statistiche** riquadro.<br><br> ![Riquadro Statistiche processi](./media/automation-runbook-execution/automation-account-job-status-summary.png).<br> Questo riquadro Visualizza un numero e la rappresentazione grafica hello lo stato del processo per tutti i processi eseguiti.  

Fare clic sul riquadro hello presenta hello **processi** pannello, che include un elenco riepilogativo di tutti i processi eseguiti, con stato, l'esecuzione del processo e ora di inizio e completamento.<br><br> ![Pannello dei processi di account di Automazione](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  È possibile filtrare l'elenco di hello dei processi selezionando **filtrare i processi** e filtrare in un runbook specifico, lo stato del processo o dall'elenco a discesa hello, hello toosearch intervallo di data/ora all'interno.<br><br> ![Filtrare lo stato dei processi](./media/automation-runbook-execution/automation-account-jobs-filter.png)

In alternativa, è possibile visualizzare i dettagli di riepilogo di processo per un runbook specifico, selezionare runbook dal hello **runbook** pannello nell'account di automazione e quindi seleziona hello **processi** riquadro.  Questa operazione presenta hello **processi** pannello e da qui è possibile fare clic su hello processo record tooview dettagli e l'output.<br><br> ![Pannello dei processi di account di Automazione](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>Riepilogo dei processi
È possibile visualizzare un elenco di tutti i processi di hello che sono stati creati per un determinato runbook e il relativo stato più recente. È possibile filtrare l'elenco per lo stato del processo e hello intervallo di date per hello ultima modifica toohello processo. tooview, output e le relative informazioni dettagliate, fare clic sul nome di hello di un processo. Hello visualizzazione dettagliata del processo di hello include valori hello per i parametri del runbook hello che sono stati forniti toothat processo.

È possibile utilizzare hello seguendo i passaggi tooview hello i processi per un runbook.

1. Nel portale di Azure hello, selezionare **automazione** e quindi selezionare il nome di hello di un account di automazione.
2. Dall'hub hello, selezionare **runbook** e quindi su hello **runbook** pannello riepilogo, selezionare un runbook hello.
3. Nel Pannello di hello per runbook hello selezionato, fare clic su hello **processi** riquadro.
4. Fare clic su uno dei processi di hello in elenco hello e nel pannello dettagli processo runbook di hello è possibile visualizzarne i dettagli e l'output.

## <a name="retrieving-job-status-using-windows-powershell"></a>Recupero dello stato di un processo tramite Windows PowerShell
È possibile utilizzare hello [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) processi di hello tooretrieve creati per un runbook e hello dettagli di un processo specifico. Se si avvia un runbook con Windows PowerShell con [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx), quindi restituisce processo risultante hello. Utilizzare [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)tooget di Output di output di un processo.

Hello comandi di esempio seguenti recuperare l'ultimo processo di hello per un runbook di esempio e visualizza il relativo stato, i valori hello forniti per i parametri di runbook hello e hello output dal processo hello.

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>condivisione equa
Nelle risorse di tooshare ordine tra tutti i runbook nel cloud hello, automazione di Azure verrà Scarica temporaneamente qualsiasi processo dopo che è in esecuzione per 3 ore.  Durante questo periodo, i processi per [runbook basati su PowerShell](automation-runbook-types.md#powershell-runbooks) vengono arrestati e non verranno riavviati.  Mostra lo stato di processo Hello **arrestato**.  Questo tipo di runbook viene sempre riavviato dall'inizio hello poiché non supportano i checkpoint.  

[I runbook basati su Workflow-PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) verranno ripresi dall'ultimo [checkpoint](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints).  Dopo aver eseguito tre ore, il processo di runbook hello verrà sospeso dal servizio hello e il relativo stato viene **in esecuzione, in attesa di risorse**.  Quando un ambiente sandbox diventa disponibile, hello runbook verrà riavviato automaticamente dal servizio di automazione hello e verrà ripreso dall'ultimo checkpoint hello.  Questo è il comportamento normale di Workflow-PowerShell per sospendere/riavviare.  Se runbook hello supera nuovamente tre ore della fase di esecuzione processo hello si ripete, i tempi di toothree.  Dopo il riavvio terzo hello, se runbook hello ancora non è stata completata in tre ore, quindi viene eseguito il processo di runbook hello e Mostra lo stato del processo hello **non riuscito, in attesa di risorse**.  In questo caso, si riceve hello con errore hello l'eccezione seguente.

*processo Hello non è possibile continuare l'esecuzione perché è stato rimosso ripetutamente da hello stesso checkpoint. Verificare che il runbook non esegua operazioni di lunga durata senza rendere persistente il proprio stato.*

Si tratta di servizio di hello tooprotect esecuzione runbook indefinitamente senza essere completati, in quanto non sono in grado di toomake è toohello checkpoint successivo senza venire scaricati di nuovo.

Se non sono presenti checkpoint hello runbook o processo hello non ha raggiunto un primo checkpoint hello prima di essere scaricato, quindi viene riavviato dall'inizio hello.  

Quando si crea un runbook, è necessario assicurarsi che toorun ora hello qualsiasi attività tra due checkpoint non superi di tre ore. Potrebbe essere necessario tooadd checkpoint tooyour runbook tooensure che non venga raggiunto questo limite di tre ore o suddividere prolungata operazioni in esecuzione. Ad esempio, il runbook potrebbe eseguire una reindicizzazione su un database SQL di grandi dimensioni. Se questa singola operazione non completata entro hello equo il limite di condivisione, quindi il processo di hello è scaricato e riavviato dall'inizio di hello. In questo caso, è necessario suddividere l'operazione di reindicizzazione hello in più passaggi, ad esempio la reindicizzazione di una tabella alla volta e quindi inserire un checkpoint dopo ogni operazione in modo che hello processo possa riprendere dopo hello ultima operazione toocomplete.

## <a name="next-steps"></a>Passaggi successivi
* toolearn informazioni su hello diversi metodi che possono essere utilizzati toostart un runbook in automazione di Azure, vedere [avvio di un runbook in automazione di Azure](automation-starting-a-runbook.md)

