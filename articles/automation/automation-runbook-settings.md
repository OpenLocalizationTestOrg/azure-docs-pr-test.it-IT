---
title: Impostazioni dei runbook | Documentazione Microsoft
description: Illustra le impostazioni di configurazione per un runbook in Automazione di Azure e come modificarle usando il portale di gestione di Azure e Windows PowerShell.
services: automation
documentationcenter: 
author: eslesar
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
ms.openlocfilehash: 534ea7e3f2f8e5640db4d351c2bb3245f29b6eec
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="runbook-settings"></a>Impostazioni dei runbook
Ogni runbook in Automazione di Azure dispone di più impostazioni che consentono di identificarlo e di modificarne il comportamento di registrazione. Per ognuna di queste impostazioni, di seguito viene riportata una descrizione e vengono illustrate le procedure di modifica.

## <a name="settings"></a>Impostazioni
### <a name="name-and-description"></a>Nome e descrizione
Non è possibile modificare il nome di un runbook dopo che è stato creato. La descrizione è facoltativa e può contenere fino a 512 caratteri.

### <a name="tags"></a>Tag
I tag consentono di assegnare parole e frasi distinte per facilitare l'identificazione di un runbook. Quando si invia un runbook alla [PowerShell Gallery](https://www.powershellgallery.com/), è possibile ad esempio specificare tag particolari per identificare le categorie in cui il runbook deve essere elencato. È possibile specificare più tag per un runbook separandole con le virgole.

### <a name="logging"></a>Registrazione
Per impostazione predefinita, i record dettagliati e di avanzamento non vengono scritti nella cronologia processo. È possibile modificare le impostazioni per un determinato runbook per registrare questi record. Per altre informazioni su tali record, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Modifica delle impostazioni dei runbook

### <a name="changing-runbook-settings-with-the-azure-portal"></a>Modifica delle impostazioni dei runbook nel portale di Azure
Per modificare le impostazioni di un runbook nel portale di Azure, usare il pannello **Impostazioni** corrispondente.

1. Nel portale di Azure selezionare **Automazione** e quindi fare clic sul nome di un account di automazione.
2. Fare clic sulla scheda **Runbook** .
3. Fare clic sul nome di un runbook per aprire il pannello delle impostazioni corrispondente. In tale pannello è possibile specificare o modificare i tag e la descrizione del runbook, configurare le impostazioni di traccia e registrazione e accedere agli strumenti di supporto per la risoluzione dei problemi.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Modifica delle impostazioni dei runbook con Windows PowerShell
Per modificare le impostazioni di un runbook, è possibile usare il cmdlet [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx). Se si intende specificare più tag, è possibile fornire una matrice o una singola stringa con valori delimitati da virgole per il parametro Tags. Per ottenere i tag correnti, usare [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

I comandi di esempio seguenti illustrano come impostare le proprietà di un runbook. Questo esempio aggiunge tre tag ai tag esistenti e specifica che vengano registrati i record dettagliati.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Passaggi successivi
* Per informazioni su come creare e recuperare l'output e i messaggi di errore da runbook, vedere [Messaggi e output del runbook](automation-runbook-output-and-messages.md). 
* Per informazioni su come aggiungere un runbook già sviluppato dalla community o da un'altra origine o su come creare runbook propri, vedere [Creazione o importazione di un runbook](automation-creating-importing-runbook.md). 

