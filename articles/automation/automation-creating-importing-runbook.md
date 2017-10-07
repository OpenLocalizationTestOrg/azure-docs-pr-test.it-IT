---
title: aaaCreating o importazione di un runbook in automazione di Azure
description: Questo articolo viene descritto come toocreate un nuovo runbook in automazione di Azure o l'importazione da un file.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>Creazione o importazione di un runbook in Automazione di Azure
È possibile aggiungere un tooAzure runbook automazione mediante [crearne uno nuovo](#creating-a-new-runbook) o importando un runbook esistente da un file o da hello [raccolta Runbook](automation-runbook-gallery.md). In questo articolo vengono fornite informazioni sulla creazione e importazione di runbook da un file.  È possibile ottenere tutti i dettagli di hello sull'accesso alla community runbook e moduli in [raccolte Runbook e moduli di automazione di Azure](automation-runbook-gallery.md).

## <a name="creating-a-new-runbook"></a>Creazione di un nuovo runbook
È possibile creare un nuovo runbook in automazione di Azure utilizzando uno dei hello Azure portali o Windows PowerShell. Dopo aver creato il runbook hello, è possibile modificarlo utilizzando le informazioni in [flusso di lavoro PowerShell Learning](automation-powershell-workflow.md) e [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md).

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>un nuovo runbook di automazione di Azure con il portale di Azure classico hello toocreate
È possibile utilizzare solo [runbook del flusso di lavoro di PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) in hello portale di Azure.

1. Nel portale di Azure classico hello, fare clic su, **New**, **servizi App**, **automazione**, **Runbook**, **Creazionerapida**.
2. Immettere le informazioni necessarie hello e quindi fare clic su **crea**. nome di runbook Hello deve iniziare con una lettera e può contenere lettere, numeri, caratteri di sottolineatura e trattini.
3. Se si desidera ora tooedit hello runbook, quindi fare clic su **modifica Runbook**. In caso contrario, fare clic su **OK**.
4. Il nuovo runbook verrà visualizzato nella hello **runbook** scheda.

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate un nuovo runbook di automazione di Azure con hello portale di Azure
1. Nel portale di Azure hello, aprire l'account di automazione.
2. Hello Hub, selezionare **runbook** elenco hello tooopen di runbook.
3. Fare clic su hello **aggiungere un runbook** pulsante e quindi **creare un nuovo runbook**.
4. Digitare un **nome** per runbook hello e selezionare il [tipo](automation-runbook-types.md). nome di runbook Hello deve iniziare con una lettera e può contenere lettere, numeri, caratteri di sottolineatura e trattini.
5. Fare clic su **crea** toocreate hello runbook ed editor hello aperto.

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate un nuovo runbook di automazione di Azure con Windows PowerShell
È possibile utilizzare hello [New AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) toocreate cmdlet vuota [runbook del flusso di lavoro di PowerShell](automation-runbook-types.md#powershell-workflow-runbooks). È possibile specificare hello **nome** parametro toocreate un runbook vuoto che è possibile modificare successivamente oppure è possibile specificare hello **percorso** parametro tooimport un file di runbook. Hello **tipo** parametro deve essere anche incluso toospecify uno dei tipi di runbook hello quattro.

Mostra i comandi di esempio seguente Hello come toocreate un nuovo runbook vuoto.

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>Importazione di un runbook da un file in Automazione di Azure
È possibile creare un nuovo runbook in Automazione di Azure mediante l'importazione di uno script di PowerShell o un flusso di lavoro di PowerShell (con estensione PS1) o un runbook grafico esportato (con estensione GRAPHRUNBOOK).  È necessario specificare hello [tipo di runbook](automation-runbook-types.md) che verrà creato dall'importazione hello tenendo hello account seguenti considerazioni.

* Un file con estensione GRAPHRUNBOOK può essere importato solo in un nuovo [runbook grafico](automation-runbook-types.md#graphical-runbooks), mentre i runbook grafici possono essere creati solo da un file con estensione GRAPHRUNBOOK.
* Un file con estensione PS1 che contiene un flusso di lavoro di PowerShell può essere importato solo in un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se il file hello contiene più flussi di lavoro di PowerShell, quindi hello importazione avrà esito negativo. È necessario salvare ogni file di flusso di lavoro tooits personalizzati e importarli separatamente.
* Un file con estensione ps1 che non contiene un flusso di lavoro può essere importato in un [runbook di PowerShell](automation-runbook-types.md#powershell-runbooks) o in un [runbook del flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks).  Se viene importato in un runbook del flusso di lavoro di PowerShell, quindi sarà convertito tooa flusso di lavoro e verranno inclusi commenti nel runbook hello specificando hello modifiche apportate.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>un runbook da un file con il portale di Azure classico hello tooimport
È possibile utilizzare hello seguendo procedure tooimport un file di script in automazione di Azure.  Si noti che è possibile importare solo un file con estensione PS1 in un runbook del flusso di lavoro PowerShell con questo portale.  Per altri tipi, è necessario utilizzare hello portale di Azure.

1. Nel portale di gestione di Azure hello selezionare **automazione** e quindi selezionare un Account di automazione.
2. Fare clic su **Importa**.
3. Fare clic su **Cerca File** e individuare tooimport file di script hello.
4. Se si desidera ora tooedit hello runbook, quindi fare clic su **modifica Runbook**. In caso contrario, fare clic su OK.
5. Hello nuovo runbook verrà visualizzato in hello **runbook** scheda hello Account di automazione.
6. È necessario [pubblicare hello runbook](#publishing-a-runbook) prima di eseguire.

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport un runbook da un file con hello portale di Azure
È possibile utilizzare hello seguendo procedure tooimport un file di script in automazione di Azure.  

> [!NOTE]
> Si noti che è possibile importare un file con estensione ps1 solo all'interno di un runbook del flusso di lavoro di PowerShell tramite il portale di hello.
> 
> 

1. Nel portale di Azure hello, aprire l'account di automazione.
2. Hello Hub, selezionare **runbook** elenco hello tooopen di runbook.
3. Fare clic su hello **aggiungere un runbook** pulsante e quindi **importazione**.
4. Fare clic su **file Runbook** tooselect hello file tooimport
5. Se hello **nome** campo è attivato e quindi aver toochange opzione hello è.  nome di runbook Hello deve iniziare con una lettera e può contenere lettere, numeri, caratteri di sottolineatura e trattini.
6. Hello [tipo runbook](automation-runbook-types.md) verrà selezionato automaticamente, ma è possibile modificare il tipo di hello dopo aver preso hello applicabile in considerazione le restrizioni. 
7. Hello nuovo runbook verrà visualizzato nell'elenco di hello di runbook per hello Account di automazione.
8. È necessario [pubblicare hello runbook](#publishing-a-runbook) prima di eseguire.

> [!NOTE]
> Dopo aver importato un runbook grafico o un runbook del flusso di lavoro di PowerShell con interfaccia grafico, è hello opzione tooconvert toohello altro tipo se si desidera. Non è possibile convertire tootextual.
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport un runbook da un file di script con Windows PowerShell
È possibile utilizzare hello [importazione AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) tooimport cmdlet un file di script come una bozza di runbook del flusso di lavoro di PowerShell. Se il runbook hello esiste già, importazione hello avrà esito negativo a meno che non si utilizza hello *-Force* parametro. 

Hello comandi di esempio seguenti Mostra come tooimport uno script del file in un runbook.

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>Pubblicazione di un runbook
Quando si crea o si importa un nuovo runbook, è necessario pubblicarlo prima di poterlo eseguire.  Ogni runbook in Automazione include una versione bozza e una versione pubblicata. Solo versione di hello pubblicato è disponibile toobe eseguire e può essere modificata solo la versione bozza hello. versione di Hello pubblicato è influenzata da una qualsiasi versione bozza toohello di modifiche. Versione bozza hello deve essere rese disponibili, è pubblicarla, sovrascrivendo così versione di hello pubblicato con la versione bozza hello.

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish un runbook con un portale di Azure classico hello
1. Aprire hello runbook nel portale di Azure classico hello.
2. In alto hello hello, fare clic su **autore**.
3. In basso hello hello, fare clic su **pubblica** e quindi **Sì** toohello messaggio di verifica.

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish un runbook con hello portale di Azure
1. Aprire il runbook hello in hello portale di Azure.
2. Fare clic su hello **modifica** pulsante.
3. Fare clic su hello **pubblica** pulsante e quindi **Sì** toohello messaggio di verifica.

## <a name="toopublish-a-runbook-using-windows-powershell"></a>toopublish un runbook con Windows PowerShell
È possibile utilizzare hello [pubblica AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) toopublish cmdlet un runbook con Windows PowerShell. Mostra i comandi di esempio seguente Hello come toopublish un runbook di esempio.

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>Passaggi successivi
* toolearn su come è possibile trarre vantaggio da hello Runbook e il modulo di PowerShell Gallery, vedere [raccolte Runbook e moduli di automazione di Azure](automation-runbook-gallery.md)
* toolearn più sulla modifica di runbook PowerShell e flusso di lavoro di PowerShell con un editor di testo, vedere [modifica testuale runbook in automazione di Azure](automation-edit-textual-runbook.md)
* toolearn più sulla creazione di runbook con interfaccia grafica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md)

