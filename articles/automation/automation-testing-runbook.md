---
title: aaaTesting un runbook in automazione di Azure | Documenti Microsoft
description: "Prima di pubblicare un runbook in automazione di Azure, è possibile eseguirne il test tooensure che funziona come previsto.  Questo articolo viene descritto come tootest un runbook e visualizzare l'output."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>Test di un runbook in Automazione di Azure
Quando si testa un runbook, hello [versione bozza](automation-creating-importing-runbook.md#publishing-a-runbook) viene eseguita e vengono completate tutte le azioni eseguite. Viene creata alcuna cronologia processo, ma hello [Output](automation-runbook-output-and-messages.md#output-stream) e [avviso ed errore](automation-runbook-output-and-messages.md#message-streams) vengono visualizzati i flussi in hello Test riquadro di output. Messaggi toohello [flusso dettagliato](automation-runbook-output-and-messages.md#message-streams) vengono visualizzate nel riquadro di Output di hello solo se hello [$VerbosePreference variabile](automation-runbook-output-and-messages.md#preference-variables) è impostato tooContinue.

Anche se è stata eseguita versione bozza hello, hello runbook eseguito normalmente del flusso di lavoro di hello, esegue eventuali azioni sulle risorse nell'ambiente di hello. Per questo motivo, è necessario testare solo runbook a risorse non di produzione.

Hello tootest procedura [tipo di runbook](automation-runbook-types.md) è hello stesso e non esiste alcuna differenza nei test dall'editor di testo hello ed editor grafico di hello in hello portale di Azure.  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>un runbook nel portale di Azure hello tootest
Può funzionare con qualsiasi [tipo runbook](automation-runbook-types.md) in hello portale di Azure.

1. Versione bozza hello aprire runbook hello in entrambi hello [editor testuale](automation-edit-textual-runbook.md) o [editor grafico](automation-graphical-authoring-intro.md).
2. Fare clic su hello **Test** pannello Test hello tooopen di pulsante.
3. Se hello runbook include parametri, questi verranno elencati nel riquadro di sinistra hello in cui è possibile fornire valori toobe utilizzato per il test di hello.
4. Se si desidera test hello toorun un [Runbook Worker ibrido](automation-hybrid-runbook-worker.md), quindi modificare **impostazioni di esecuzione** troppo**Worker ibrido** e hello selezionare il nome del gruppo di destinazione hello.  In caso contrario, mantenere predefinito hello **Azure** toorun hello test nel cloud hello.
5. Fare clic su hello **avviare** test hello toostart di pulsante.
6. Se il runbook hello è [flusso di lavoro PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) o [Graphical](automation-runbook-types.md#graphical-runbooks), è possibile arrestare o sospendere viene testato con pulsanti hello sotto il riquadro di Output di hello. Quando si sospende il runbook hello, viene completata l'attività corrente hello prima della sospensione. Dopo aver sospeso hello runbook, è possibile arrestarlo o riavviarlo.
7. Esaminare l'output di hello da hello runbook nel riquadro di output di hello.

## <a name="next-steps"></a>Passaggi successivi
* toolearn toocreate o importare un runbook, vedere [creazione o importazione di un runbook in automazione di Azure](automation-creating-importing-runbook.md)
* toolearn ulteriori informazioni sui grafici per la modifica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md)
* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
* toolearn ulteriori informazioni sul runboks tooreturn messaggi di stato e gli errori, incluse le procedure consigliate, vedere [Runbook output e i messaggi in automazione di Azure](automation-runbook-output-and-messages.md)

