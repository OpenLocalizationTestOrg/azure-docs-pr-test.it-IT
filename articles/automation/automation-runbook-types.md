---
title: Tipi di automazione Runbook aaaAzure | Documenti Microsoft
description: "Descrive i diversi tipi di hello di runbook che è possibile utilizzare in automazione di Azure e le considerazioni da tenere in considerazione per determinare quali toouse di tipo. "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Tipi di runbook di Automazione di Azure
Automazione di Azure supporta quattro tipi di runbook che sono descritte brevemente nella tabella seguente hello.  Nelle sezioni seguenti Hello forniscono ulteriori informazioni su ogni tipo, con alcune considerazioni su quando toouse ogni.

| Tipo | Descrizione |
|:--- |:--- |
| [Grafico](#graphical-runbooks) |Basato su Windows PowerShell e creato e modificato completamente nell'editor grafico nel portale di Azure. |
| [Grafico del flusso di lavoro di PowerShell](#graphical-runbooks) |Basata sul flusso di lavoro di Windows PowerShell e un editor grafico di hello creato e modificato completamente nel portale di Azure. |
| [PowerShell](#powershell-runbooks) |Runbook di testo basato su script di Windows PowerShell. |
| [Flusso di lavoro PowerShell](#powershell-workflow-runbooks) |Runbook di testo basato su flusso di lavoro Windows PowerShell. |

## <a name="graphical-runbooks"></a>Runbook grafici
[Grafica](automation-runbook-types.md#graphical-runbooks) e runbook del flusso di lavoro di PowerShell con interfaccia grafica vengono creati e modificati con l'editor grafico di hello in hello portale di Azure.  È possibile esportarli tooa file e quindi importarli in un altro account di automazione, ma non è possibile creare o modificare con un altro strumento.  I runbook grafici generano il codice di PowerShell, ma non è possibile direttamente consente di visualizzare o modificare il codice hello. I runbook grafici non possono essere convertito tooone di hello [formati di testo](automation-runbook-types.md), né un runbook di testo è possibile convertire toographical formato. I runbook grafici possono essere convertiti tooGraphical runbook del flusso di lavoro di PowerShell durante l'importazione e viceversa.

### <a name="advantages"></a>Vantaggi
* Modello di creazione con inserimento, collegamento e configurazione visivi  
* Lo stato attivo sulla modalità di flusso di dati tramite il processo di hello  
* Rappresentazione visiva dei processi di gestione  
* Includere altri runbook come figlio runbook toocreate alto livello dei flussi di lavoro  
* Agevolazione della programmazione modulare  


### <a name="limitations"></a>Limitazioni
* Impossibilità di modificare il runbook all'esterno del portale di Azure.
* Potrebbe essere necessario una logica complessa PowerShell codice tooperform contenente un'attività del codice.
* Non è possibile visualizzare o modificare direttamente il codice di PowerShell hello creato dal flusso di lavoro grafico hello. Si noti che è possibile visualizzare codice hello creato in qualsiasi attività di codice.

## <a name="powershell-runbooks"></a>Runbook di PowerShell
I runbook di PowerShell sono basati su Windows PowerShell.  Modificare direttamente il codice di hello di runbook hello editor di testo hello in hello portale di Azure.  È inoltre possibile utilizzare qualsiasi editor di testo non in linea e [importare runbook hello](http://msdn.microsoft.com/library/azure/dn643637.aspx) in automazione di Azure.

### <a name="advantages"></a>Vantaggi
* Implementare la logica complessa tutti con codice di PowerShell senza ulteriori complessità di hello del flusso di lavoro di PowerShell. 
* Runbook avvia più velocemente rispetto ai runbook del flusso di lavoro di PowerShell perché non è necessario che toobe compilato prima dell'esecuzione.

### <a name="limitations"></a>Limitazioni
* Necessità di familiarità con la scrittura di script di PowerShell.
* Non è possibile utilizzare [l'elaborazione parallela](automation-powershell-workflow.md#parallel-processing) tooperform più operazioni in parallelo.
* Non è possibile utilizzare [checkpoint](automation-powershell-workflow.md#checkpoints) runbook tooresume in caso di errore.
* Runbook del flusso di lavoro di PowerShell e runbook grafici possono solo essere inclusi come runbook figlio tramite il cmdlet Start-AzureAutomationRunbook hello che crea un nuovo processo.

### <a name="known-issues"></a>Problemi noti
Di seguito sono descritti i problemi noti correnti relativi ai runbook di PowerShell.

* I runbook di PowerShell non sono in grado di recuperare un [asset di tipo variabile](automation-variables.md) non crittografato con valore Null.
* I runbook di PowerShell non è possibile recuperare un [asset della variabile](automation-variables.md) con  *~*  nel nome hello.
* Get-Process in un ciclo in un runbook di PowerShell può arrestarsi in modo anomalo dopo circa 80 iterazioni. 
* Un runbook PowerShell potrebbe non riuscire se tenta toowrite una quantità elevata di flusso di output toohello dei dati in una sola volta.   È possibile risolvere questo problema in genere restituendo solo informazioni di hello che è necessario quando si utilizzano oggetti di grandi dimensioni.  Ad esempio, anziché l'output simile al seguente *Get-Process*, è possibile restituire solo i campi necessario hello con *Get-Process | Selezionare ProcessName, CPU*.

## <a name="powershell-workflow-runbooks"></a>Runbook del flusso di lavoro PowerShell
I runbook del flusso di lavoro PowerShell sono runbook di testo basati sul [flusso di lavoro Windows PowerShell](automation-powershell-workflow.md).  Modificare direttamente il codice di hello di runbook hello editor di testo hello in hello portale di Azure.  È inoltre possibile utilizzare qualsiasi editor di testo non in linea e [importare runbook hello](http://msdn.microsoft.com/library/azure/dn643637.aspx) in automazione di Azure.

### <a name="advantages"></a>Vantaggi
* Implementazione di tutta la logica complessa con codice del flusso di lavoro PowerShell.
* Utilizzare [checkpoint](automation-powershell-workflow.md#checkpoints) runbook tooresume in caso di errore.
* Utilizzare [l'elaborazione parallela](automation-powershell-workflow.md#parallel-processing) tooperform più operazioni in parallelo.
* Può includere altri runbook grafici e i runbook del flusso di lavoro di PowerShell come figlio runbook toocreate elevata livello flussi di lavoro.

### <a name="limitations"></a>Limitazioni
* Necessità che l'autore abbia familiarità con il flusso di lavoro PowerShell.
* Runbook deve affrontare complessità hello del flusso di lavoro di PowerShell, ad esempio [deserializzare gli oggetti](automation-powershell-workflow.md#code-changes).
* Runbook prende toostart più tempo rispetto ai runbook PowerShell poiché deve toobe compilato prima dell'esecuzione.
* Runbook PowerShell possono solo essere inclusi come runbook figlio tramite il cmdlet Start-AzureAutomationRunbook hello che crea un nuovo processo.

## <a name="considerations"></a>Considerazioni
È opportuno tenere in hello account seguenti considerazioni aggiuntive per determinare quali toouse di tipo per un runbook specifico.

* I runbook non è possibile convertire dal tipo di grafico tootextual o viceversa.
* Esistono limitazioni di uso dei runbook di tipi diversi come runbook figlio.  Per altre informazioni, vedere [Runbook figlio in Automazione di Azure](automation-child-runbooks.md) .

## <a name="next-steps"></a>Passaggi successivi
* toolearn più sulla creazione di runbook con interfaccia grafica, vedere [grafici per la modifica in automazione di Azure](automation-graphical-authoring-intro.md)
* hello toounderstand le differenze tra PowerShell e PowerShell flussi di lavoro per runbook, vedere [il flusso di lavoro di apprendimento Windows PowerShell](automation-powershell-workflow.md)
* Per ulteriori informazioni su come toocreate o importare un Runbook, vedere [creazione o importazione di un Runbook](automation-creating-importing-runbook.md)

