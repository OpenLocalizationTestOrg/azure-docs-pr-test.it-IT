---
title: Modifica di runbook testuali in Automazione di Azure
description: In questo articolo vengono fornite procedure diverse per l'uso di PowerShell e dei runbook del flusso di lavoro PowerShell in Automazione di Azure mediante l'editor di testo.
services: automation
documentationcenter: 
author: eslesar
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
ms.openlocfilehash: ae36342ab0f42c364dedd4107a59f5b0ffc20a0a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>Modifica di runbook testuali in Automazione di Azure
L'editor di testo in Automazione di Azure può essere usato per modificare i [runbook di PowerShell](automation-runbook-types.md#powershell-runbooks) e i [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). Questo editor dispone delle funzionalità tipiche degli altri editor di codice, ad esempio IntelliSense e la codifica a colori con particolari funzionalità aggiuntive per semplificare l'accesso alle risorse comuni dei runbook.  In questo articolo vengono fornite procedure dettagliate per l'esecuzione delle diverse funzioni disponibili in questo editor.

L'editor di testo include una funzionalità per inserire codice per attività, risorse e runbook figlio all'interno di un runbook. Invece di digitare il codice manualmente, è possibile effettuare selezioni in un elenco di risorse disponibili e inserire automaticamente il codice nel runbook.

Ogni runbook in Automazione di Azure include due versioni, ovvero una versione bozza e una versione pubblicata. Si modifica la versione bozza del runbook e quindi lo si pubblica in modo da poterlo eseguire. La versione pubblicata non può essere modificata. Per altre informazioni, vedere [Pubblicazione di un runbook](automation-creating-importing-runbook.md#publishing-a-runbook) .

Per usare i [runbook grafici](automation-runbook-types.md#graphical-runbooks), vedere [Creazione grafica in Automazione di Azure](automation-graphical-authoring-intro.md).

## <a name="to-edit-a-runbook-with-the-azure-portal"></a>Per modificare un runbook con il portale di Azure
Usare la procedura seguente per aprire un runbook per la modifica nell'editor di testo.

1. Nel portale di Azure selezionare l'account di automazione.
2. Fare clic nel pannello **Runbook** per aprire l'elenco dei runbook.
3. Fare clic sul nome del runbook che si desidera modificare e quindi fare clic sul pulsante **Modifica** .
4. Apportare le modifiche necessarie.
5. Fare clic su **Salva** dopo aver completato le modifiche desiderate.
6. Fare clic su **Pubblica** se si desidera pubblicare la versione bozza più recente del runbook.

### <a name="to-insert-a-cmdlet-into-a-runbook"></a>Per inserire un cmdlet in un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire il cmdlet.
2. Espandere il nodo **Cmdlet** nel controllo della libreria.
3. Espandere il modulo contenente il cmdlet che si desidera usare.
4. Fare clic con il pulsante destro sul cmdlet da inserire e selezionare **Aggiungi a canvas**.  Se il cmdlet include più di un set di parametri, verrà aggiunto il set predefinito.  È inoltre possibile espandere il cmdlet per selezionare un set di parametri diverso.
5. Il codice per il cmdlet viene inserito con l'intero elenco di parametri.
6. Fornire un valore appropriato al posto del tipo di dati racchiuso tra parentesi graffe <> per gli eventuali parametri obbligatori.  Rimuovere i parametri non necessari.

### <a name="to-insert-code-for-a-child-runbook-into-a-runbook"></a>Per inserire il codice per un runbook figlio all'interno di un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire il codice per il [runbook figlio](automation-child-runbooks.md).
2. Espandere il nodo **Runbook** nel controllo della libreria.
3. Fare clic con il pulsante destro sul runbook da inserire e selezionare **Aggiungi a canvas**.
4. Il codice relativo al runbook figlio viene inserito con qualsiasi segnaposto necessario per i parametri del runbook.
5. Sostituire i segnaposto con i valori appropriati per ogni parametro.

### <a name="to-insert-an-asset-into-a-runbook"></a>Per inserire un asset in un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire il codice per il runbook figlio.
2. Espandere il nodo **Asset** nel controllo della libreria.
3. Espandere il nodo per il tipo di asset desiderato.
4. Fare clic con il pulsante destro sull'asset da inserire e selezionare **Aggiungi a canvas**.  Per gli [asset di tipo variabile](automation-variables.md), selezionare l'opzione **Aggiungi "Ottieni variabile" a canvas** o **Aggiungi "Imposta variabile" a canvas** a seconda che si desideri ottenere o impostare la variabile.
5. Il codice per l'asset viene inserito nel runbook.

## <a name="to-edit-a-runbook-with-the-azure-portal"></a>Per modificare un runbook con il portale di Azure
Usare la procedura seguente per aprire un runbook per la modifica nell'editor di testo.

1. Nel portale di Azure selezionare **Automazione** e quindi fare clic sul nome di un account di automazione.
2. Fare clic sulla scheda **Runbook** .
3. Fare clic sul nome del runbook che si desidera modificare e quindi selezionare la scheda **Creazione** .
4. Fare clic sul pulsante **Modifica** nella parte inferiore della schermata.
5. Apportare le modifiche necessarie.
6. Fare clic su **Salva** dopo aver completato le modifiche desiderate.
7. Fare clic su **Pubblica** se si desidera pubblicare la versione bozza più recente del runbook.

### <a name="to-insert-an-activity-into-a-runbook"></a>Per inserire un'attività in un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire l'attività.
2. Nella parte inferiore della schermata fare clic su **Inserisci** e su **Attività**.
3. Nella colonna **Modulo di integrazione** selezionare il modulo che contiene l'attività.
4. Nel riquadro **Attività** selezionare un'attività.
5. Nella colonna **Descrizione** annotare la descrizione dell'attività. Facoltativamente, è possibile fare clic su Visualizza Guida dettagliata per avviare la Guida relativa all'attività nel browser.
6. Fare clic sulla freccia destra.  Se l'attività dispone di parametri, questi verranno elencati come riferimento.
7. Fare quindi clic sul pulsante con il segno di spunta.  Il codice per l'esecuzione dell'attività verrà inserito nel runbook.
8. Se l'attività richiede parametri, fornire un valore appropriato al posto del tipo di dati racchiuso tra parentesi graffe <>.

### <a name="to-insert-code-for-a-child-runbook-into-a-runbook"></a>Per inserire il codice per un runbook figlio all'interno di un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire il [runbook figlio](automation-child-runbooks.md).
2. Nella parte inferiore della schermata fare clic su **Inserisci** e su **Runbook**.
3. Selezionare il runbook da inserire nella colonna centrale e fare clic sulla freccia a destra.
4. Se il runbook dispone di parametri, questi verranno elencati come riferimento.
5. Fare quindi clic sul pulsante con il segno di spunta.  Il codice per l'esecuzione del runbook selezionato verrà inserito nel runbook corrente.
6. Se il runbook richiede parametri, fornire un valore appropriato al posto del tipo di dati racchiuso tra parentesi graffe <>.

### <a name="to-insert-an-asset-into-a-runbook"></a>Per inserire un asset in un runbook
1. Nel canvas dell'editor di testo posizionare il cursore nel punto in cui si desidera inserire l'attività per recuperare l'asset.
2. Nella parte inferiore della schermata fare clic su **Inserisci** e su **Impostazione**.
3. Nella colonna **Azione impostazione** selezionare l'azione desiderata.
4. Effettuare una selezione tra gli asset disponibili nella colonna centrale.
5. Fare quindi clic sul pulsante con il segno di spunta.  Il codice per ottenere o impostare l'asset verrà inserito nel runbook.

## <a name="to-edit-an-azure-automation-runbook-using-windows-powershell"></a>Per modificare un runbook di Automazione di Azure tramite Windows PowerShell
Per modificare un runbook con Windows PowerShell, usare l'editor desiderato e salvarlo in un file con estensione PS1. È possibile usare il cmdlet [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) per recuperare il contenuto del runbook e quindi il cmdlet [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) per sostituire la versione bozza del runbook esistente con quello modificato.

### <a name="to-retrieve-the-contents-of-a-runbook-using-windows-powershell"></a>Per recuperare il contenuto di un runbook con Windows PowerShell
I comandi di esempio seguenti mostrano come recuperare lo script per un runbook e salvarlo in un file di script. In questo esempio viene recuperata la versione bozza. È inoltre possibile recuperare la versione pubblicata del runbook, sebbene questa versione non possa essere modificata.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="to-change-the-contents-of-a-runbook-using-windows-powershell"></a>Per modificare il contenuto di un Runbook con Windows PowerShell
I comandi di esempio seguenti mostrano come sostituire il contenuto di un runbook con il contenuto di un file di script. Si noti che questa è la stessa procedura di esempio descritta in [Per importare un runbook da un file di script con Windows PowerShell](automation-creating-importing-runbook.md).

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
