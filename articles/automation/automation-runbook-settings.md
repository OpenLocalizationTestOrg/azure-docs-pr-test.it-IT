---
title: impostazioni aaaRunbook | Documenti Microsoft
description: Vengono descritte le impostazioni di configurazione hello per un runbook in automazione di Azure e come toochange sia mediante hello portale di gestione di Azure e Windows PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Impostazioni dei runbook
Ogni runbook in automazione di Azure dispone di più impostazioni che consentono di toobe identificato e toochange relativo comportamento di registrazione. Ognuna di queste impostazioni è descritta di seguito seguita da procedure su come toomodify li.

## <a name="settings"></a>Impostazioni
### <a name="name-and-description"></a>Nome e descrizione
È possibile modificare il nome di hello di un runbook dopo che è stato creato. Hello descrizione è facoltativo e può essere di too512 caratteri.

### <a name="tags"></a>Tag
Tag consentono il che identificazione di un runbook è tooassign parole e frasi toohelp. Ad esempio, quando si invia un toohello runbook [PowerShell Gallery](https://www.powershellgallery.com/), si specifica tooidentify tag particolari quali categorie hello runbook dovrebbe essere elencato. È possibile specificare più tag per un runbook separandole con le virgole.

### <a name="logging"></a>Registrazione
Per impostazione predefinita, i record dettagliati e di avanzamento non vengono scritte toojob cronologia. È possibile modificare le impostazioni di hello per un determinato runbook di toolog questi record. Per altre informazioni su tali record, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Modifica delle impostazioni dei runbook

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Modifica delle impostazioni di runbook con hello portale di Azure
È possibile modificare le impostazioni per un runbook nel portale di Azure hello da hello **impostazioni** pannello per il runbook hello.

1. Nel portale di Azure hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.
2. Seleziona hello **runbook** scheda.
3. Fare clic sul nome di un runbook hello e si è il pannello impostazioni toohello diretto per hello runbook. Da qui è possibile specificare o modificare i tag, hello descrizione del runbook, configura la registrazione e le impostazioni di traccia e toohelp di strumenti di supporto risolvere i problemi di accesso.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Modifica delle impostazioni dei runbook con Windows PowerShell
È possibile utilizzare hello [Set AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) impostazioni hello toochange di cmdlet per un runbook. Se si desidera toospecify più tag, è possibile fornire una matrice o una singola stringa con il parametro di tag toohello valori delimitati da virgole. È possibile ottenere i tag corrente hello con hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Hello comandi di esempio seguenti Mostra come tooset hello proprietà di un runbook. In questo esempio aggiunge tre tag esistenti toohello tag e specifica che i record dettagliati devono essere registrati.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Passaggi successivi
* toolearn toocreate e recuperare messaggi di errore e di output dal runbook, vedere [Runbook Output and Messages](automation-runbook-output-and-messages.md) 
* vedere un runbook che è stato già sviluppato da hello community o altra origine o toocreate propri runbook tooadd toounderstand [la creazione o importazione di un Runbook](automation-creating-importing-runbook.md) 

