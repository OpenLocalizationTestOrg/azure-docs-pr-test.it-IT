---
title: runbook testuale aaaEditing in automazione di Azure
description: In questo articolo vengono fornite procedure diverse per l'utilizzo di PowerShell e flusso di lavoro PowerShell runbook in automazione di Azure utilizzando l'editor di testo hello.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Modifica di runbook testuali in Automazione di Azure
Hello editor di testo in automazione di Azure può essere utilizzato tooedit [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) e [runbook del flusso di lavoro di PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Questo include funzionalità tipiche di hello di altri editor di codice, ad esempio intellisense e di codifica a colori con altre funzionalità speciali tooassist è l'accesso a risorse comuni toorunbooks.  In questo articolo vengono fornite procedure dettagliate per l'esecuzione delle diverse funzioni disponibili in questo editor.

editor di testo Hello include un codice di tooinsert funzionalità per le attività, risorse e i runbook figlio in un runbook. Anziché digitare hello codice manualmente, è possibile selezionare da un elenco di risorse disponibili e codice appropriato di hello inserito nel runbook hello.

Ogni runbook in Automazione di Azure include due versioni, ovvero una versione bozza e una versione pubblicata. Si modifica la versione di hello bozza di runbook hello e quindi pubblicarlo in modo da poter essere eseguito. versione di Hello pubblicato non può essere modificata. Per altre informazioni, vedere [Pubblicazione di un runbook](automation-creating-importing-runbook.md#publishing-a-runbook) .

toowork con [runbook grafici](automation-runbook-types.md#graphical-runbooks), vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook con hello portale di Azure
Utilizzare hello seguendo procedure tooopen un runbook per la modifica nell'editor di testo hello.

1. Nel portale di Azure hello, selezionare l'account di automazione.
2. Fare clic su hello **runbook** riquadro tooopen hello elenco di runbook.
3. Fare clic sul nome hello di runbook hello tooedit desiderato e quindi fare clic su hello **modifica** pulsante.
4. Eseguire hello richiesto la modifica.
5. Fare clic su **Salva** dopo aver completato le modifiche desiderate.
6. Fare clic su **pubblica** se si desidera hello bozza più recente di hello runbook toobe pubblicato.

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert un cmdlet in un runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore hello in cui si desidera tooplace hello cmdlet.
2. Espandere hello **cmdlet** nodo hello controllo della raccolta.
3. Espandere il modulo di hello contenente i cmdlet di hello desiderato toouse.
4. Fare clic con il pulsante destro tooinsert cmdlet hello e selezionare **aggiungere toocanvas**.  Se il cmdlet hello più di un parametro impostato, verrà aggiunto set predefinito di hello.  È anche possibile espandere hello cmdlet tooselect un parametro differente impostato.
5. codice Hello per cmdlet hello viene inserito con l'intero elenco di parametri.
6. Fornire un valore appropriato al posto di tipo di dati hello racchiuso tra parentesi graffe <> per eventuali parametri obbligatori.  Rimuovere i parametri non necessari.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>codice tooinsert per un runbook figlio in un runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore di hello laddove si voglia ottenere codice hello tooplace per hello [runbook figlio](automation-child-runbooks.md).
2. Espandere hello **runbook** nodo hello controllo della raccolta.
3. Fare clic con il pulsante destro tooinsert runbook hello e selezionare **aggiungere toocanvas**.
4. codice Hello per runbook figlio hello viene inserito con tutti i segnaposto per i parametri di runbook.
5. Sostituire i segnaposto hello con valori appropriati per ogni parametro.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un asset in un runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore hello laddove si voglia ottenere codice hello tooplace per runbook figlio hello.
2. Espandere hello **asset** nodo hello controllo della raccolta.
3. Espandere il nodo di hello per il tipo di hello di asset desiderato.
4. Fare clic con il pulsante destro tooinsert asset hello e selezionare **aggiungere toocanvas**.  Per [gli asset variabili](automation-variables.md), selezionare l'opzione **Aggiungi "Ottieni variabile" toocanvas** o **Aggiungi "Imposta variabile" toocanvas** a seconda che si desidera tooget oppure impostare la variabile hello.
5. codice di Hello per asset hello è inserito nel runbook hello.

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit un runbook con hello portale di Azure
Utilizzare hello seguendo procedure tooopen un runbook per la modifica nell'editor di testo hello.

1. Nel portale di Azure hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.
2. Seleziona hello **runbook** scheda.
3. Fare clic sul nome hello di runbook hello tooedit desiderato e quindi selezionare hello **autore** scheda.
4. Fare clic su hello **modifica** pulsante in basso hello hello.
5. Eseguire hello richiesto la modifica.
6. Fare clic su **Salva** dopo aver completato le modifiche desiderate.
7. Fare clic su **pubblica** se si desidera hello bozza più recente di hello runbook toobe pubblicato.

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert un'attività in un Runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore hello in cui si desidera che tooplace hello attività.
2. In basso hello hello, fare clic su **inserire** e quindi **attività**.
3. In hello **modulo di integrazione** colonna, il modulo hello select che contiene attività hello.
4. In hello **attività** riquadro, selezionare un'attività.
5. In hello **descrizione** colonna Descrizione hello nota dell'attività hello. Facoltativamente, è possibile fare clic su visualizzazione dettagliata della Guida per l'attività hello in browser hello. toolaunch.
6. Fare clic sulla freccia a destra di hello.  Se hello attività include parametri, questi verranno elencati a scopo informativo.
7. Controllo pulsante hello.  Attività di hello toorun codice verrà inserito nel runbook hello.
8. Se l'attività hello richiede parametri, inserire un valore appropriato al posto di tipo di dati hello racchiuso tra parentesi graffe <>.

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>codice tooinsert per un runbook figlio in un runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore di hello in cui si desidera hello tooplace [runbook figlio](automation-child-runbooks.md).
2. In basso hello hello, fare clic su **inserire** e quindi **Runbook**.
3. Selezionare hello runbook tooinsert dalla colonna centrale hello e fare clic sulla freccia a destra di hello.
4. Se hello runbook include parametri, questi verranno elencati a scopo informativo.
5. Controllo pulsante hello.  Codice toorun hello selezionato runbook verrà inserito nel runbook corrente hello.
6. Se hello runbook richiede parametri, inserire un valore appropriato al posto di tipo di dati hello racchiuso tra parentesi graffe <>.

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert un asset in un runbook
1. Nell'area di disegno dell'editor di testo hello hello, posizionare il cursore hello in cui si desidera asset hello tooretrieve di tooplace hello attività.
2. In basso hello hello, fare clic su **inserire** e quindi **impostazione**.
3. In hello **azione impostazione** azione selezionare hello che si desidera, di colonna.
4. Selezionare le risorse disponibili nella colonna centrale hello hello.
5. Controllo pulsante hello.  Codice tooget o set hello asset verrà inserito nel runbook hello.

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit un runbook di automazione di Azure con Windows PowerShell
tooedit un runbook con Windows PowerShell, è possibile utilizzare hello editor di propria scelta e salvarlo come file con estensione ps1 tooa. È possibile utilizzare hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) contenuto hello tooretrieve di cmdlet di hello runbook e quindi [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello esistente modifica del runbook bozza con hello uno.

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello contenuto di un Runbook usando Windows PowerShell
Hello comandi di esempio seguenti Mostra come tooretrieve hello script per un runbook e salvarlo come file di script tooa. In questo esempio viene recuperata versione bozza hello. È anche possibile tooretrieve di hello runbook attuale versione pubblicato hello ma questa versione non può essere modificata.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello contenuto di un Runbook usando Windows PowerShell
Hello comandi di esempio seguenti mostrano come tooreplace hello contenuto esistente di un runbook con il contenuto di hello di un file di script. Si noti che questo è hello stessa routine come nell'esempio [tooimport un runbook da un file di script con Windows PowerShell](automation-creating-importing-runbook.md).

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>Articoli correlati
* [Creazione o importazione di un runbook in Automazione di Azure](automation-creating-importing-runbook.md)
* [Informazioni sul flusso di lavoro PowerShell](automation-powershell-workflow.md)
* [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md)
* [Certificati](automation-certificates.md)
* [Connessioni](automation-connections.md)
* [Credenziali](automation-credentials.md)
* [Pianificazioni](automation-schedules.md)
* [Variabili](automation-variables.md)
