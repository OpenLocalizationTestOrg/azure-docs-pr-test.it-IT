---
title: aaaManaging dati di automazione di Azure | Documenti Microsoft
description: "Questo articolo contiene più argomenti per la gestione di un ambiente di Automazione di Azure.  Include attualmente conservazione dei dati e backup del ripristino di emergenza di Automazione di Azure in Automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Gestione dei dati di Automazione di Azure
Questo articolo contiene più argomenti per la gestione di un ambiente di Automazione di Azure.

## <a name="data-retention"></a>Conservazione dei dati
Quando si elimina una risorsa in Automazione di Azure, i dati corrispondenti vengono conservati per 90 giorni per finalità di controllo, prima della rimozione permanente.  È possibile visualizzare o usare risorse hello durante questo periodo.  Questo criterio si applica anche tooresources appartenenti tooan account di automazione che viene eliminato.

Automazione di Azure elimina automaticamente e rimuove definitivamente i processi dopo 90 giorni.

Hello nella tabella seguente sono riepilogati i criteri di conservazione hello per le diverse risorse.

| Dati | Criterio |
|:--- |:--- |
| Account |Rimossi in modo permanente 90 giorni dopo l'eliminazione dell'account hello da un utente. |
| Asset |Rimossi in modo permanente 90 giorni dopo l'eliminazione dell'asset hello da un utente o 90 giorni dopo hello account che possiede l'asset hello viene eliminato da un utente. |
| Moduli |Rimossi in modo permanente 90 giorni dopo l'eliminazione del modulo hello da un utente o 90 giorni dopo hello account che contiene il modulo hello viene eliminato da un utente. |
| Runbook |Rimossi in modo permanente 90 giorni dopo l'eliminazione della risorsa hello da un utente o 90 giorni dopo hello account che possiede la risorsa hello viene eliminato da un utente. |
| Processi |Eliminati e rimossi definitivamente 90 giorni dopo l'ultima modifica, Potrebbe trattarsi di processo hello al termine, è stato arrestato o è stato sospeso. |
| Configurazioni di nodo/File MOF |La configurazione di nodo precedente verrà rimossa definitivamente 90 giorni dopo che viene generata una nuova configurazione di nodo. |
| Nodi DSC |Rimossi in modo permanente 90 giorni dopo il nodo hello è stato annullato dall'Account di automazione con il portale di Azure o hello [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) cmdlet in Windows PowerShell. I nodi vengono rimossi anche in modo permanente 90 giorni dopo l'account di hello che contiene il nodo di hello viene eliminato da un utente. |
| Report sul nodo |Vengono rimossi in modo permanente 90 giorni dopo la generazione di un nuovo report per quel nodo |

criteri di conservazione Hello applica tooall utenti e attualmente non è possibile personalizzare.

Tuttavia, se è necessario tooretain dati per un periodo di tempo, è possibile inoltrare runbook processo registri tooLog Analitica.  Per ulteriori informazioni, vedere [inoltrare tooOMS dati di automazione di Azure processo Analitica Log](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Backup di Automazione di Azure
Quando si elimina un account di automazione di Microsoft Azure, vengono eliminati tutti gli oggetti nell'account hello inclusi runbook, moduli, configurazioni, le impostazioni, processi e risorse. Impossibile ripristinare gli oggetti Hello dopo l'eliminazione di account hello.  È possibile utilizzare hello seguente contenuto hello toobackup di informazioni dell'account di automazione prima di eliminarlo. 

### <a name="runbooks"></a>Runbook
È possibile esportare i file di tooscript runbook utilizzando il portale di gestione di Azure hello o hello [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) cmdlet in Windows PowerShell.  Questi file di script possono essere importati in un account di Automazione, come illustrato in [Creazione o importazione di un Runbook](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Moduli di integrazione
Non è possibile esportare i moduli di integrazione da Automazione di Azure.  È necessario assicurarsi che siano disponibili di fuori di account di automazione hello.

### <a name="assets"></a>Asset
Non è possibile esportare [asset](https://msdn.microsoft.com/library/dn939988.aspx) da Automazione di Azure.  Tramite il portale di gestione di Azure hello, annotare i dettagli di hello di variabili, le credenziali, certificati, connessioni e pianificazioni.  È quindi necessario creare manualmente eventuali asset usati dai Runbook importati in un altro account di Automazione.

È possibile utilizzare [i cmdlet di Azure](https://msdn.microsoft.com/library/dn690262.aspx) dettagli di tooretrieve di asset non crittografato e salvarli per futuro riferimento o creare risorse equivalenti in un altro account di automazione.

È possibile recuperare il valore di hello per le variabili crittografate o un campo di hello password delle credenziali mediante i cmdlet.  Se non si conoscono questi valori, quindi sarà possibile recuperarli da un runbook con hello [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) e [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) le attività.

Non è possibile esportare certificati da Automazione di Azure.  È necessario assicurarsi che eventuali certificati siano disponibili all'esterno di Azure.

### <a name="dsc-configurations"></a>Configurazioni DSC
È possibile esportare i file di tooscript configurazioni utilizzando il portale di gestione di Azure hello o hello [esportazione AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) cmdlet in Windows PowerShell. Queste configurazioni possono essere importate e usate in un altro account di automazione.

## <a name="geo-replication-in-azure-automation"></a>Replica geografica in Automazione di Azure
Replica geografica standard negli account di automazione di Azure, il backup account dati tooa area geografica diversa per la ridondanza. Quando si configura l'account, è possibile scegliere un'area primaria e quindi un'area secondaria viene assegnata automaticamente tooit. dati secondari Hello, copiati dall'area primaria hello, viene continuamente aggiornati in caso di perdita di dati.  

Hello nella tabella seguente mostra hello associazioni di aree primarie e secondarie disponibili.

| Primario | Secondaria |
| --- | --- |
| Stati Uniti centro-meridionali |Stati Uniti centro-settentrionali |
| Stati Uniti orientali 2 |Stati Uniti centrali |
| Europa occidentale |Europa settentrionale |
| Asia sudorientale |Asia orientale |
| Giappone orientale |Giappone occidentale |

In caso di guasto hello la perdita dei dati di un area primaria, Microsoft tenta toorecover è. Se non è possibile recuperare dati primario hello, viene eseguito il failover geo e hello clienti verranno informati su questo tramite la sottoscrizione a pagamento.

