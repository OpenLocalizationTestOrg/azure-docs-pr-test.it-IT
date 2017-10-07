---
title: gestione nei runbook di automazione di Azure con interfaccia grafico aaaError | Documenti Microsoft
description: Questo articolo viene descritto come errore tooimplement logica nei runbook di automazione di Azure con interfaccia grafica di gestione.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Gestione degli errori nei runbook grafici di Automazione di Azure

Una progettazione di runbook chiave principale tooconsider prevede l'identificazione diversi problemi che potrebbe verificarsi un runbook. ad esempio problemi relativi a esito positivo o negativo, stati di errore previsti e condizioni di errori imprevisti.

I runbook devono includere logica di gestione degli errori. toovalidate hello output di un'attività o gestire un errore con i runbook grafici, è Impossibile utilizzare un'attività di codice Windows PowerShell, definire la logica condizionale nel collegamento di output di hello dell'attività hello o applicare un altro metodo.          

Spesso, se si verifica un errore non irreversibile che si verifica con un'attività del runbook, qualsiasi attività che segue viene elaborata indipendentemente dall'errore hello. Errore Hello è probabilmente toogenerate un'eccezione, ma l'attività successiva hello è comunque consentita toorun. Questo è il modo di hello che PowerShell è progettato toohandle errori.    

tipi di errori di PowerShell che possono verificarsi durante l'esecuzione di Hello sono interruzione o non irreversibile. differenze di Hello tra gli errori di interruzione e non definitive sono i seguenti:

* **Errore fatale**: un errore grave durante l'esecuzione si ferma completamente, il comando hello (o l'esecuzione dello script). Gli esempi includono cmdlet inesistenti, errori di sintassi che impediscono l'esecuzione di un cmdlet o altri errori irreversibili.

* **Errore non irreversibile**: un errore non grave che consente l'esecuzione toocontinue nonostante l'errore hello. Gli esempi includono errori operativi come errori di file non trovati e problemi relativi alle autorizzazioni.

Automazione di Azure sono stati migliorati i runbook grafici hello funzionalità tooinclude la gestione degli errori. È ora possibile trasformare le eccezioni in errori non irreversibili e creare collegamenti di errori tra le attività. Questo processo consente a un autore runbook toocatch errori e gestire le condizioni realizzate o impreviste.  

## <a name="when-toouse-error-handling"></a>Quando la gestione degli errori toouse

Ogni volta che è un'attività critica che genera un errore o eccezione, è importante tooprevent hello attività successiva del runbook dall'errore hello toohandle e l'elaborazione, in modo appropriato. Questo è essenziale soprattutto quando i runbook supportano un processo correlato alle operazioni aziendali o di servizio.

Per ogni attività in grado di produrre un errore, autore runbook hello possibile aggiungere un collegamento all'errore che punta tooany altre attività.  attività di destinazione Hello possono essere di qualsiasi tipo, incluse le attività di codice, la chiamata di un cmdlet, richiamare un altro runbook e così via.

In attività di destinazione hello può inoltre essere collegamenti in uscita. che possono essere collegamenti normali o collegamenti di errore. Ciò significa che l'autore runbook hello può implementare la logica di gestione degli errori complessa senza ricorrere tooa attività del codice. Hello consigliato è toocreate un runbook di gestione degli errori dedicato con le funzionalità comuni, ma non è obbligatorio. La logica di gestione degli errori in un'attività di codice di PowerShell non è hello solo l'opzione.  

Ad esempio, si consideri un runbook che tenta di toostart una macchina virtuale e installare un'applicazione su di esso. Se hello VM non viene avviato correttamente, esegue due azioni:

1. Invio di una notifica relativa al problema.
2. Avvio di un altro runbook che effettua automaticamente il provisioning di una nuova macchina virtuale.

Una soluzione è toohave un collegamento all'errore che punta tooan attività che gli handle di passaggio uno. Ad esempio, è possibile connettersi hello **Write-Warning** cmdlet tooan attività per il passaggio 2, ad esempio hello **inizio AzureRmAutomationRunbook** cmdlet.

È anche possibile generalizzare questo comportamento per l'uso nei runbook molti inserendo queste due attività in un runbook di gestione degli errori separata e linee guida seguenti di hello suggerito in precedenza. Prima di chiamare questo runbook di gestione degli errori, è possibile costruire un messaggio personalizzato da dati hello in runbook originale hello e passarla come un runbook di gestione degli errori di parametro toohello.

## <a name="how-toouse-error-handling"></a>La modalità di gestione degli errori toouse

Ogni attività ha un'impostazione di configurazione che trasforma le eccezioni in errori non irreversibili. Per impostazione predefinita, questa impostazione è disabilitata. È consigliabile abilitare questa impostazione in qualsiasi attività in cui si desidera che gli errori toohandle.  

Abilitando questa configurazione, sono garantire che gli errori di interruzione e non irreversibile nell'attività hello vengono gestiti come errori non irreversibili che possono essere gestiti con un collegamento all'errore.  

Dopo aver configurato questa impostazione, si crea un'attività che gestisce gli errori di hello. Se un'attività genera un errore, quindi hello in uscita di errore vengono seguiti i collegamenti e hello regolare i collegamenti sono, anche se l'attività hello produce anche output regolare.<br><br> ![Esempio di collegamento di errore in un runbook di Automazione](media/automation-runbook-graphical-error-handling/error-link-example.png)

Nel seguente esempio di hello, un runbook recupera una variabile che contiene il nome computer hello di una macchina virtuale. Tenta quindi di macchina virtuale di hello toostart con attività successiva hello.<br><br> ![Esempio di gestione degli errori in un runbook di Automazione](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

Hello **Get-AutomationVariable** attività e **inizio AzureRmVm** sono tooerrors eccezioni tooconvert configurato.  Se sono presenti problemi di funzionamento hello iniziale o variabile hello macchina virtuale, quindi vengono generati errori.<br><br> ![Impostazioni delle attività di gestione degli errori in un runbook di Automazione](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

Flusso di errore collegamenti da questi tooa attività singola **la gestione degli errori** attività (un'attività del codice). Questa attività è configurata con un'espressione PowerShell semplice che utilizza hello *generare* toostop (parola chiave) l'elaborazione, insieme con *$Error.Exception.Message* tooget messaggio che descrive hello eccezione corrente.<br><br> ![Esempio di codice di gestione degli errori in un runbook di Automazione](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>Passaggi successivi

* toolearn ulteriori informazioni sui collegamenti e i tipi di collegamento nei runbook con interfaccia grafico, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md#links-and-workflow).

* ulteriori sull'esecuzione di runbook, come i processi del runbook toomonitor e altri dettagli tecnici, vedere toolearn [tenere traccia di un processo del runbook](automation-runbook-execution.md).
