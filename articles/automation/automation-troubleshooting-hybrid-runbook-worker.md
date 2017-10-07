---
title: aaaTroubleshoot Runbook Worker ibrido automazione di Azure | Documenti Microsoft
description: "Vengono descritti hello sintomi, cause e risoluzione dei problemi più comuni di lavoro ibridi per Runbook in automazione di Azure hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: magoedte
ms.openlocfilehash: 292af517c88d1ffd21262a286ccc079e7270bfad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-tips-for-hybrid-runbook-worker"></a>Consigli per la risoluzione dei problemi del ruolo di lavoro ibrido per runbook

Questo articolo vengono fornite indicazioni sulla risoluzione degli errori si possono verificarsi con i Runbook worker ibridi di automazione e vengono suggerite le possibili soluzioni tooresolve li.

## <a name="a-runbook-job-terminates-with-a-status-of-suspended"></a>Un processo runbook termina con lo stato Sospeso

Il runbook viene sospeso subito dopo il tentativo di tooexecute è tre volte. Sono presenti condizioni che potrebbero interrompere hello runbook venga completato correttamente e il messaggio di errore correlati hello non include informazioni aggiuntive che indica il motivo. In questo articolo vengono fornite procedure per errori di esecuzione di runbook di problemi correlati toohello Runbook Worker ibrido.

Se il problema di Azure non viene risolto in questo articolo, visitare hello forum di Azure in [MSDN e hello Overflow dello Stack](https://azure.microsoft.com/support/forums/). È possibile registrare il problema in questi forum o troppo[ @AzureSupport su Twitter](https://twitter.com/AzureSupport). Inoltre, è possibile inviare una richiesta di supporto tecnico di Azure selezionando **ottenere supporto** su hello [supporto tecnico di Azure](https://azure.microsoft.com/support/options/) sito.

### <a name="symptom"></a>Sintomo
Esecuzione del runbook ha esito negativo ed errore hello, "hello azione del processo 'Activate' può essere eseguita perché l'arresto imprevisto del processo hello. azione del processo Hello è stata tentata 3 volte."

Esistono diverse cause di errore hello: 

1. thread di lavoro ibridi Hello è dietro un proxy o firewall
2. Hello di lavoro ibridi hello computer è in esecuzione su è minore di hello minimo [requisiti hardware](automation-offering-get-started.md#hybrid-runbook-worker)  
3. i runbook Hello non possono autenticarsi con risorse locali

#### <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Causa 1: il ruolo di lavoro ibrido per runbook è protetto da firewall o proxy
hello computer Hello in che runbook Worker ibrido è in esecuzione si trova dietro un firewall o proxy server e accesso alla rete in uscita non può essere consentito o configurato correttamente.

#### <a name="solution"></a>Soluzione
Verificare i computer di hello disponga dell'accesso in uscita too*.azure-automation.net sulla porta 443. 

#### <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Causa 2: il computer non soddisfa i requisiti hardware minimi
I computer che eseguono lavoro ibridi per Runbook deve soddisfare hello hello requisiti hardware minimi prima designazione di toohost questa funzionalità. In caso contrario, a seconda di hello utilizzo delle risorse di altri processi in background e contesa causata da runbook durante l'esecuzione, hello computer verranno diventano sovraccarico e causare ritardi processo runbook o i timeout. 

#### <a name="solution"></a>Soluzione
Confermare il computer di hello designato funzionalità di Runbook Worker ibrido hello toorun soddisfi i requisiti hardware minimi hello.  In caso affermativo, monitorare eventuali correlazioni tra le prestazioni di hello di processi di lavoro ibridi per Runbook e Windows toodetermine di utilizzo della CPU e memoria.  Se è presente memoria o a utilizzo elevato della CPU, questo potrebbe indicare tooupgrade necessità hello o aggiungere processori aggiuntivi o aumento della memoria tooaddress hello collo di bottiglia e risolvere l'errore hello. In alternativa, selezionare una risorsa di calcolo diversi che può supportare i requisiti minimi di hello e scalabilità quando le richieste di carico di lavoro indicano che un aumento è necessario.         

#### <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Causa 3: i runbook non possono autenticarsi con le risorse locali

#### <a name="solution"></a>Soluzione
Controllare hello **Microsoft SMA** registro eventi per un evento corrispondente con descrizione *Win32 processo terminato con codice [4294967295]*.  causa Hello di questo errore è l'utente non configurata l'autenticazione dei runbook o hello credenziali runas per il gruppo di lavoro ibridi hello specificato.  Consultare [autorizzazioni Runbook](automation-hrw-run-runbooks.md#runbook-permissions) tooconfirm è stato configurato correttamente l'autenticazione per i runbook.  

## <a name="next-steps"></a>Passaggi successivi

Per informazioni sulla risoluzione di altri problemi di Automazione, vedere [Risoluzione dei problemi comuni di Automazione di Azure](automation-troubleshooting-automation-errors.md) 