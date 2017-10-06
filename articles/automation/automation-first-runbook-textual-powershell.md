---
title: aaaMy primo PowerShell runbook in automazione di Azure | Documenti Microsoft
description: Esercitazione viene illustrata la creazione di hello, test e la pubblicazione di un runbook semplice di PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: Azure PowerShell, esercitazione sugli script di PowerShell, automazione di PowerShell
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>Il primo runbook PowerShell

> [!div class="op_single_selector"]
> * [Grafico](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [Flusso di lavoro PowerShell](automation-first-runbook-textual.md)
> 
> 

In questa esercitazione viene illustrata la creazione hello di un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) in automazione di Azure. Si inizia con un runbook semplice test e pubblicare mentre spiegheremo come tootrack hello lo stato di processo del runbook hello. È modificare runbook hello tooactually Gestione risorse di Azure, in questo caso, avviare una macchina virtuale di Azure. Infine, si rende hello runbook più affidabile mediante l'aggiunta di parametri del runbook.

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario hello seguenti:

* Sottoscrizione di Azure. Se non si ha ancora una sottoscrizione, è possibile [attivare i vantaggi della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure <a href="/pricing/free-account/" target="_blank">[iscriversi per ottenere un account gratuito](https://azure.microsoft.com/free/).
* [Account di automazione](automation-sec-configure-azure-runas-account.md) toohold hello runbook ed eseguire l'autenticazione tooAzure risorse.  Questo account deve disporre dell'autorizzazione toostart e arrestare la macchina virtuale hello.
* Macchina virtuale di Azure. La macchina virtuale viene arrestata e avviata, quindi non deve essere una macchina virtuale di produzione.

## <a name="step-1---create-new-runbook"></a>Passaggio 1: Creare nuovo runbook
Si inizierà creando un runbook semplice che restituisce testo hello *Hello World*.

1. Nel portale di Azure hello, aprire l'account di automazione.  
   pagina account di automazione Hello offre una rapida panoramica delle risorse hello in questo account. Dovrebbero essere già disponibili alcuni asset. La maggior parte di questi sono i moduli di hello che vengono inclusi automaticamente in un nuovo account di automazione. È inoltre necessario avere asset delle credenziali hello menzionato in hello [prerequisiti](#prerequisites).
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. Creare un nuovo runbook, fare clic su hello **aggiungere un runbook** pulsante e quindi **creare un nuovo runbook**.
4. Nome di hello runbook hello *MyFirstRunbook PowerShell*.
5. In questo caso, verrà toocreate un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) pertanto selezionare **Powershell** per **tipo Runbook**.<br><br> ![Tipo di runbook](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. Fare clic su **crea** toocreate hello runbook ed editor di testo hello aperto.

## <a name="step-2---add-code-toohello-runbook"></a>Passaggio 2: aggiungere codice toohello runbook
È possibile scrivere codice di tipo direttamente nel runbook hello, o è possibile selezionare i cmdlet, i runbook e le risorse da hello controllo della raccolta e li aggiunto toohello runbook con i parametri correlati. Questa procedura dettagliata, si digita direttamente nel runbook hello.

1. Il runbook è attualmente vuoto, digitare *Write-Output "Hello World"*.<br><br> ![Hello World](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. Salvare il runbook hello facendo **salvare**.<br><br> ![Pulsante Salva](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>Passaggio 3: Test hello runbook
Prima Pubblichiamo toomake runbook hello è disponibile nell'ambiente di produzione, è necessario tootest è toomake assicurarsi che funzioni correttamente. Quando si testa un runbook, è necessario eseguire la versione **Bozza** e visualizzarne l'output in modo interattivo.

1. Fare clic su **riquadro Test** riquadro Test di tooopen hello.<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. Fare clic su **avviare** test hello toostart. Deve trattarsi di opzione hello solo abilitato.
3. Viene creato un [processo del runbook](automation-runbook-execution.md) e il relativo stato viene visualizzato.  
   lo stato del processo Hello viene avviato come *in coda* che indica che è in attesa per un runbook worker in hello cloud toocome disponibili. Verranno quindi spostati troppo*iniziale* quando un thread di lavoro attestazioni processo hello e quindi *esecuzione* quando runbook hello effettivamente avviata l'esecuzione.  
4. Al termine del processo del runbook hello, viene visualizzato l'output. In questo caso, dovrebbe essere visualizzato *Hello World*.<br><br> ![Output del Riquadro test](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. Chiudere l'area di disegno hello Test riquadro tooreturn toohello.

## <a name="step-4---publish-and-start-hello-runbook"></a>Passaggio 4: pubblicare e avviare runbook hello
runbook Hello creata è ancora in modalità bozza. È necessario toopublish prima di poterlo eseguire nell'ambiente di produzione.  Quando si pubblica un runbook, con la versione bozza hello sovrascrivere versione hello già pubblicata.  In questo caso, non abbiamo una versione pubblicata ancora poiché runbook hello appena creato.

1. Fare clic su **pubblica** toopublish hello runbook e quindi **Sì** quando richiesto.<br><br> ![Pulsante Publish](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. Se si scorre tooview sinistro hello runbook hello **runbook** riquadro a questo punto, verrà visualizzato un **stato di creazione** di **pubblicato**.
3. Riquadro destro tooview hello toohello indietro di scorrimento per **MyFirstRunbook PowerShell**.  
   Hello opzioni in alto hello consentono toostart hello runbook, visualizzare hello runbook, pianificarlo toostart in un momento nel futuro hello o creare un [webhook](automation-webhooks.md) in modo da poter essere avviato tramite una chiamata HTTP.
4. Si desidera toostart hello runbook, quindi fare clic su **avviare** e quindi fare clic su **Ok** quando si apre Pannello avvia Runbook hello.<br><br> ![Pulsante Avvia](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. Il riquadro di un processo viene aperto per il processo di runbook hello creati. È possibile chiudere questo riquadro, ma in questo caso viene lasciato aperto in modo è possibile controllare lo stato di avanzamento del processo di hello.
6. viene visualizzato lo stato del processo Hello in **riepilogo** e corrispondenze hello gli Stati che abbiamo visto quando è stato testato hello runbook.<br><br> ![Riepilogo dei processi](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. Una volta hello Mostra lo stato runbook *completato*, fare clic su **Output**. viene aperto il riquadro di Output di Hello e possiamo vedere nostri *Hello World*.<br><br> ![Output processo](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. Riquadro di Output di hello Chiudi.
9. Fare clic su **tutti i log** tooopen hello flussi riquadro processo del runbook hello. Solo dovremmo vedere *Hello World* nell'output di hello flusso, tuttavia questa operazione consente di visualizzare i flussi per un processo del runbook, ad esempio dettagliati e di errore se runbook hello scrive toothem.<br><br> ![Tutti i log](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. Chiudere il riquadro di flussi hello e hello processo tooreturn toohello MyFirstRunbook PowerShell un riquadro.
11. Fare clic su **processi** riquadro processi di hello tooopen per questo runbook. Elenca tutti i processi di hello creati da questo runbook. Dovremmo vedere solo un processo elencato in quanto è solo esecuzione hello processo una volta.<br><br> ![Elenco processi](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. È possibile fare clic su questo processo tooopen hello stesso riquadro processo che abbiamo visto quando è stato avviato il runbook hello. In questo modo si toogo indietro nel tempo e visualizzarne i dettagli di hello di qualsiasi processo che è stato creato per un runbook specifico.

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>Passaggio 5: aggiungere l'autenticazione toomanage risorse di Azure
Il runbook è stato testato e pubblicato, ma finora non esegue alcuna attività utile. Vogliamo toohave Gestione risorse di Azure. Non sarà in grado di toodo che anche se a meno che non è necessario autenticare utilizzando credenziali hello cui hello tooin [prerequisiti](#prerequisites). Facciamo con hello **Aggiungi AzureRmAccount** cmdlet.

1. Editor di testo hello aprire facendo clic su **modifica** nel riquadro di hello MyFirstRunbook PowerShell.<br><br> ![Modifica runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. Non è necessario hello **Write-Output** più di riga, faccio, quindi eliminarlo.
3. Digitare o copiare e incollare hello seguente di codice che gestisce l'autenticazione con l'account RunAs automazione hello:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. Fare clic su **riquadro Test** in modo che sia possibile testare il runbook hello.
5. Fare clic su **avviare** test hello toostart. Una volta che è stata completata, si dovrebbe ricevere toohello simili di output seguente, la visualizzazione di informazioni di base dal proprio account. Questo conferma che credenziali hello sono valido.<br><br> ![Autentica](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>Passaggio 6: aggiungere codice toostart una macchina virtuale
Ora che il runbook esegue l'autenticazione tooour sottoscrizione di Azure, è possibile gestire le risorse. Aggiungere un toostart comando una macchina virtuale. È possibile scegliere qualsiasi macchina virtuale nella sottoscrizione di Azure e per il momento verranno impostare come hardcoded tale nome nei runbook hello.

1. Dopo aver *Aggiungi AzureRmAccount*, tipo *inizio AzureRmVM-Name 'VMName' - ResourceGroupName 'NameofResourceGroup'* fornendo hello nome e il nome di gruppo di risorse di hello toostart di macchina virtuale.  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. Salvare il runbook hello e quindi fare clic su **riquadro Test** in modo che è possibile eseguirne il test.
3. Fare clic su **avviare** test hello toostart. Una volta che è stata completata, verificare che la macchina virtuale hello è stata avviata.

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>Passaggio 7: aggiungere un runbook toohello parametro di input
Il runbook viene avviato attualmente hello virtuale del computer che è hardcoded hello runbook, ma sarebbe più utile se si specifica macchina virtuale hello quando hello runbook viene avviato. A questo punto sarà necessario aggiungere parametri di input toohello runbook tooprovide tale funzionalità.

1. Aggiungere parametri per *VMName* e *ResourceGroupName* toohello runbook e utilizzare queste variabili con hello **inizio AzureRmVM** cmdlet come esempio hello seguente.  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. Salvare il runbook hello e aprire il riquadro di Test hello. È ora possibile fornire valori per hello due variabili di input utilizzati nel test hello.
3. Riquadro Test hello Chiudi.
4. Fare clic su **pubblica** la nuova versione hello toopublish di hello runbook.
5. Arrestare la macchina virtuale hello che è stato avviato nel passaggio precedente hello.
6. Fare clic su **avviare** toostart hello runbook. Tipo di hello **VMName** e **ResourceGroupName** per la macchina virtuale hello che sarà toostart.<br><br> ![Passare i parametri](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Al termine del processo di runbook hello, verificare che la macchina virtuale hello è stata avviata.

## <a name="differences-from-powershell-workflow"></a>Differenze rispetto al flusso di lavoro PowerShell
I runbook di PowerShell sono hello stesso ciclo di vita, funzionalità e la gestione come runbook del flusso di lavoro di PowerShell, ma esistono alcune differenze e limitazioni:

1. Esecuzione dei runbook di PowerShell tooPowerShell confrontati veloce runbook del flusso di lavoro come non dispongono di passaggio di compilazione.
2. Runbook del flusso di lavoro di PowerShell supporta i checkpoint, utilizzare i checkpoint, i runbook del flusso di lavoro di PowerShell possono riprendere da qualsiasi punto nel runbook hello mentre runbook PowerShell è possibile riprendere solo dall'inizio hello.
3. I runbook Flusso di lavoro PowerShell supportano l'esecuzione seriale e parallela, mentre i runbook PowerShell possono eseguire i comandi solo in modo seriale.
4. In un runbook Flusso di lavoro PowerShell un'attività, un comando o un blocco di script può avere un proprio spazio di esecuzione, mentre in un runbook PowerShell tutti gli elementi in uno script vengono eseguiti in un singolo spazio di esecuzione. Esistono anche [differenze di sintassi](https://technet.microsoft.com/magazine/dn151046.aspx) tra un runbook PowerShell nativo e un runbook Flusso di lavoro PowerShell.

## <a name="next-steps"></a>Passaggi successivi
* tooget avviato con runbook grafici, vedere [il primo runbook grafico](automation-first-runbook-graphical.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
* tooknow ulteriori informazioni sui tipi di runbook, i relativi vantaggi e limitazioni, vedere [tipi di runbook di automazione di Azure](automation-runbook-types.md)
* Per altre informazioni sulla funzionalità di supporto degli script PowerShell, vedere il blog relativo al [supporto di script PowerShell nativi in Automazione di Azure](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

