---
title: Il primo runbook del flusso di lavoro di PowerShell in Automazione di Azure | Documentazione Microsoft
description: Esercitazione in cui viene illustrata la creazione, il test e la pubblicazione di un semplice runbook testuale con flusso di lavoro PowerShell.
services: automation
documentationcenter: 
author: eslesar
manager: jwhit
editor: 
keywords: PowerShell flusso di lavoro, esempi di flusso di lavoro PowerShell, flusso di lavoro PowerShell
ms.assetid: 0002d7f7-e2b5-46e3-b5eb-4596b84fd526
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/31/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 71fba79804e4361fd731ec5627526beafa01fa3b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="my-first-powershell-workflow-runbook"></a>Il primo runbook del flusso di lavoro PowerShell

> [!div class="op_single_selector"]
> * [Grafico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flusso di lavoro PowerShell](automation-first-runbook-textual.md)
> * [Python](automation-first-runbook-textual-python2.md)
> 
> 

Questa esercitazione illustra la creazione di un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) in Automazione di Azure. Si inizia con un runbook semplice che viene testato e pubblicato, quindi viene illustrato come tenere traccia dello stato del processo del runbook. Si modifica quindi il runbook per gestire effettivamente le risorse di Azure, avviando in questo caso una macchina virtuale di Azure. Si rende infine il runbook più affidabile aggiungendo i relativi parametri.

## <a name="prerequisites"></a>Prerequisiti
Per completare l'esercitazione, sono necessari gli elementi seguenti:

* Sottoscrizione di Azure. Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi dell'abbonamento MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* [Account di Automazione](automation-offering-get-started.md) che conterrà il runbook ed eseguirà l'autenticazione con le risorse di Azure.  Questo account deve avere l'autorizzazione per avviare e arrestare la macchina virtuale.
* Macchina virtuale di Azure. La macchina virtuale viene arrestata e avviata, quindi non deve essere una macchina virtuale di produzione.

## <a name="step-1---create-new-runbook"></a>Passaggio 1: Creare nuovo runbook
Si inizierà creando un runbook semplice che restituisce il testo *Hello World*.

1. Nel portale di Azure aprire l'account di automazione.  
   La pagina dell'account di automazione offre una visualizzazione rapida delle risorse di questo account. Dovrebbero essere già disponibili alcuni asset. Per la maggior parte sono i moduli inclusi automaticamente in un nuovo account di automazione. Dovrebbe essere disponibile anche l'asset credenziali citato nei [prerequisiti](#prerequisites).
2. Fare clic sul riquadro **Runbook** per aprire l'elenco dei runbook.<br><br> ![Controllo Runbook](media/automation-first-runbook-textual/runbooks-control-tiles.png)
3. Creare un nuovo runbook facendo clic sul pulsante **Aggiungi Runbook** e quindi su **Crea un nuovo runbook**.
4. Denominare il runbook *MyFirstRunbook-Workflow*.
5. In questo caso si sta creando un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks), quindi selezionare **Flusso di lavoro PowerShell** per **Tipo di Runbook**.<br><br> ![Nuovo runbook](media/automation-first-runbook-textual/new-runbook-properties.png)
6. Fare clic su **Crea** per creare il runbook e aprire l'editor di testo.

## <a name="step-2---add-code-to-the-runbook"></a>Passaggio 2: - aggiungere un codice al runbook
È possibile digitare il codice direttamente nel runbook, oppure è possibile selezionare i cmdlet, i runbook e le risorse dal controllo della libreria e aggiungerle al runbook con tutti i parametri correlati. Per questa procedura dettagliata, si digiterà direttamente nel runbook.

1. Il runbook è attualmente vuoto con solo la parola chiave richiesta *workflow* , il nome del runbook e le parentesi graffe che racchiuderanno l'intero flusso di lavoro.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   }
   ```
2. Digitare *Write-Output "Hello World".* tra parentesi graffe.

   ```
   Workflow MyFirstRunbook-Workflow
   {
   Write-Output "Hello World"
   }
   ```
3. Salvare il runbook facendo clic su **Salva**.<br><br> ![Salvataggio del runbook](media/automation-first-runbook-textual/automation-runbook-edit-controls-save.png)

## <a name="step-3---test-the-runbook"></a>Passaggio 3: Testare il runbook
Prima di pubblicare il runbook per renderlo disponibile nell'ambiente di produzione, occorre testarlo per verificare che funzioni correttamente. Quando si testa un runbook, è necessario eseguire la versione **Bozza** e visualizzarne l'output in modo interattivo.

1. Fare clic su **Pannello di test** per aprire il pannello di test.<br><br> ![Pannello di test](media/automation-first-runbook-textual/automation-runbook-edit-controls-test.png)
2. Fare clic su **Avvia** per avviare il test. Questa deve essere l'unica opzione abilitata.
3. Viene creato un [processo del runbook](automation-runbook-execution.md) e il relativo stato viene visualizzato.  
   Lo stato del processo verrà avviato come *In coda* per indicare che è in attesa della disponibilità di un thread di lavoro del runbook nel cloud. Lo stato passerà quindi ad *Avvio in corso* quando un ruolo di lavoro richiede il processo e quindi a *In esecuzione* quando l'esecuzione del runbook viene effettivamente avviata.  
4. Al termine del processo del runbook, viene visualizzato l'output. In questo caso, dovrebbe essere visualizzato *Hello World*.<br><br> ![Hello World](media/automation-first-runbook-textual/test-output-hello-world.png)
5. Chiudere il riquadro di test per tornare all'area di disegno.

## <a name="step-4---publish-and-start-the-runbook"></a>Passaggio 4: Pubblicare e avviare il runbook
Il runbook appena creato è ancora in modalità Bozza. È necessario pubblicarlo prima di poterlo eseguire in produzione. Quando si pubblica un runbook, è possibile sovrascrivere la versione pubblicata esistente con la versione bozza. In questo caso, non esiste ancora una versione pubblicata perché il runbook è appena stato creato.

1. Fare clic su **Pubblica** per pubblicare il runbook, quindi su **Sì** quando richiesto.<br><br> ![Pubblica](media/automation-first-runbook-textual/automation-runbook-edit-controls-publish.png)
2. Se ora si scorre verso sinistra per visualizzare il runbook nel pannello **Runbook**, come **Stato di creazione** viene visualizzato **Pubblicato**.
3. Scorrere verso destra per visualizzare il pannello **MyFirstRunbook-Workflow**.  
   Le opzioni nella parte superiore consentono di avviare il runbook, pianificarlo per avviarlo in qualsiasi momento in futuro o creare un [webhook](automation-webhooks.md) per poterlo avviare con una chiamata HTTP.
4. Si vuole solo avviare il runbook, quindi fare clic su **Avvia** e poi su **Sì** quando richiesto.<br><br> ![Avvia runbook](media/automation-first-runbook-textual/automation-runbook-controls-start.png)
5. Viene aperto un riquadro del processo per il processo del runbook appena creato. È possibile chiudere questo riquadro, ma in questo caso lo si lascerà aperto per poter controllare l'avanzamento del processo.
6. Lo stato del processo è visualizzato in **Riepilogo processi** e corrisponde agli stati osservati quando è stato testato il runbook.<br><br> ![Riepilogo processi](media/automation-first-runbook-textual/job-pane-status-blade-jobsummary.png)
7. Quando lo stato del runbook risulta *Completato*fare clic su **Output**. Viene aperto il pannello Output dove si può vedere il testo *Hello World*.<br><br> ![Riepilogo dei processi](media/automation-first-runbook-textual/job-pane-status-blade-outputtile.png)  
8. Chiudere il riquadro Output.
9. Fare clic su **Tutti i log** per aprire il riquadro Flussi relativo al processo del runbook. Nel flusso di output dovrebbe essere visibile solo *Hello World* , ma potrebbero essere visualizzati altri flussi per un processo del runbook, ad esempio Verbose ed Error se il runbook scrive in questi flussi.<br><br> ![Riepilogo dei processi](media/automation-first-runbook-textual/job-pane-status-blade-alllogstile.png)
10. Chiudere il riquadro dei flussi e il riquadro dei processi per tornare al riquadro MyFirstRunbook.
11. Fare clic su **Processi** per aprire il pannello dei processi per questo runbook. Sono elencati tutti i processi creati da questo runbook. Dovrebbe essere elencato un solo processo, perché il processo è stato eseguito una sola volta.<br><br> ![Processi](media/automation-first-runbook-textual/runbook-control-job-tile.png)
12. È possibile fare clic su questo processo per aprire lo stesso riquadro del processo visualizzato quando è stato avviato il runbook. In questo modo è possibile tornare indietro nel tempo e visualizzare i dettagli di tutti i processi creati per un runbook particolare.

## <a name="step-5---add-authentication-to-manage-azure-resources"></a>Passaggio 5: Aggiungere l'autenticazione per gestire le risorse di Azure
Il runbook è stato testato e pubblicato, ma finora non esegue alcuna attività utile. Si vuole fare in modo che gestisca le risorse di Azure. Sarà tuttavia in grado di eseguire questa operazione solo dopo aver fatto in modo che esegua l'autenticazione con le credenziali indicate nei [prerequisiti](#prerequisites). A questo scopo si userà il cmdlet **Add-AzureRmAccount** .

1. Aprire l'editor di testo facendo clic su **Modifica** nel pannello MyFirstRunbook-Workflow.<br><br> ![Modificare il runbook](media/automation-first-runbook-textual/automation-runbook-controls-edit.png)
2. Non è più necessaria la riga **Write-Output** , quindi andare avanti ed eliminarla.
3. Posizionare il cursore su una riga vuota tra parentesi graffe.
4. Digitare o copiare e incollare il codice seguente che gestirà l'autenticazione con l'account RunAs di Automazione:

   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
5. Fare clic sul **Pannello di test** in modo da testare il runbook.
6. Fare clic su **Avvia** per avviare il test. Al termine verrà visualizzato un output simile al seguente, con le informazioni di base sull'account. Questo conferma che la credenziale è valida.<br><br> ![Autentica](media/automation-first-runbook-textual/runbook-auth-output.png)

## <a name="step-6---add-code-to-start-a-virtual-machine"></a>Passaggio 6 - aggiungere il codice per avviare una macchina virtuale
Ora che il runbook esegue l'autenticazione per la sottoscrizione di Azure è possibile gestire le risorse. Si aggiunge un comando per avviare una macchina virtuale. È possibile selezionare una macchina virtuale qualsiasi nella sottoscrizione di Azure. Per ora il nome sarà hardcoded nel runbook.

1. Dopo *Add-AzureRmAccount* digitare *Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'NameofResourceGroup'* specificando il nome e il nome del gruppo di risorse della macchina virtuale da avviare.  

   ```
   workflow MyFirstRunbook-Workflow
   {
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   }
   ```
2. Salvare il runbook e poi fare clic su **Pannello di Test** in modo da poterne eseguire il test.
3. Fare clic su **Avvia** per avviare il test. Dopo aver completato l'attività, controllare che la macchina virtuale sia stata avviata.

## <a name="step-7---add-an-input-parameter-to-the-runbook"></a>Passaggio 7: Aggiungere un parametro di input al runbook
Ora il runbook avvia la macchina virtuale specificata nel runbook, ma sarebbe più utile se si potesse specificare la macchina virtuale quando si avvia il runbook. Per fornire questa funzionalità, ora si aggiungeranno dei parametri di input al runbook.

1. Aggiungere parametri per *VMName* e *ResourceGroupName* al runbook e usare queste variabili con il cmdlet **Start-AzureRmVM** come nell'esempio seguente.

   ```
   workflow MyFirstRunbook-Workflow
   {
    Param(
     [string]$VMName,
     [string]$ResourceGroupName
    )  
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   }
   ```
2. Salvare il runbook e aprire il riquadro Test. Si noti che ora è possibile fornire i valori per le due variabili di input che verranno usate nel test.
3. Chiudere il riquadro Test.
4. Fare clic su **Pubblica** per pubblicare la nuova versione del runbook.
5. Arrestare la macchina virtuale avviata nel passaggio precedente.
6. Fare clic su **Avvia** per avviare il runbook. Digitare **VMName** e **ResourceGroupName** per la macchina virtuale da avviare.<br><br> ![Start Runbook](media/automation-first-runbook-textual/automation-pass-params.png)<br>  
7. Quando il runbook viene completato, controllare che la macchina virtuale sia stata avviata.  

## <a name="next-steps"></a>Passaggi successivi
* Per iniziare a usare runbook grafici, vedere [Il primo runbook grafico](automation-first-runbook-graphical.md)
* Per iniziare a usare runbook del flusso di lavoro PowerShell, vedere [Il primo runbook PowerShell](automation-first-runbook-textual-powershell.md)
* Per altre informazioni sui tipi di runbook, i relativi vantaggi e le limitazioni, vedere [Tipi di runbook di Automazione di Azure](automation-runbook-types.md)
* Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [supporto di script PowerShell nativi in Automazione di Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)
